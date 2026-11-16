# Identificadores brasileiros de dados pessoais: formatos, dígitos verificadores, regex, mascaramento e bibliotecas (ref. novembro/2026)

> Notas de pesquisa para a skill de segurança/LGPD. Metodologia: (a) buscas web; (b) leitura direta do código-fonte atual (clones `--depth 1` feitos em 16/11/2026) de `validate-docbr` (v2.0.1, último commit 01/10/2026), `@brazilian-utils/brazilian-utils` JS (v2.5.0, commit 09/10/2026), `brutils-python` (v2.5.0, commit 29/10/2026), Microsoft Presidio (commit `fd78e97`, 14/11/2026), gitleaks e detect-secrets; (c) execução local de implementações Python de referência contra vetores de teste conhecidos (resultados abaixo). **Limitação importante:** nesta sessão os hosts `www.gov.br` e `microsoft.github.io` estavam bloqueados para fetch, então PDFs oficiais da Receita/BCB/TSE/MS não puderam ser lidos na íntegra; dados oficiais vêm de snippets de busca que citam esses documentos e de código de bibliotecas que citam as normas. Itens sem fonte verificada nesta sessão estão marcados **[NÃO VERIFICADO]** e/ou em "Gaps".

---

## 1. Especificação por identificador (formato, tamanho, DV, regex, falsos positivos, máscara)

### Takeaway
Quase todos os identificadores numéricos brasileiros usam variantes de **módulo 11** (CPF, CNPJ, PIS/NIT, CNH, Título, RENAVAM, CNS, Certidão) e se sobrepõem em tamanho (11 dígitos = CPF, PIS/NIT, CNH, RENAVAM; 14 = CNPJ e trechos de boleto), então **regex sozinha gera muitos falsos positivos — detecção confiável exige regex + validação de DV + palavras-chave de contexto**. O CNPJ alfanumérico (IN RFB 2.229/2024) está em vigor desde julho/2026 (primeiro emitido em 31/07/2026: `00.000.000/E08G-12`) e usa o mesmo módulo 11, convertendo cada caractere por `ASCII − 48` (0–9 → 0–9; A–Z → 17–42); os dois DVs continuam numéricos.

### Cited Findings

#### 1.1 CPF (Cadastro de Pessoas Físicas)
- Formato `NNN.NNN.NNN-DD`, 11 dígitos; 9 de base + 2 DVs. DV1: pesos 10..2 sobre os 9 primeiros; DV2: pesos 11..2 sobre os 10 primeiros; resto `r = soma % 11`, DV = `0 se r < 2, senão 11 − r`. Sequências repetidas (000…, 111…) são rejeitadas pelas bibliotecas — [brazilian-utils/javascript `is-valid-cpf`](https://github.com/brazilian-utils/javascript/tree/main/src/is-valid-cpf); [validate-docbr CPF.py](https://github.com/alvarofpp/validate-docbr/blob/main/validate_docbr/CPF.py)
- O **9º dígito indica a região fiscal** de emissão (ex.: DF/GO/MT/MS/TO = 1; AC/AM/AP/PA/RO/RR = 2; CE/MA/PI = 3; AL/PB/PE/RN = 4; BA/SE = 5; MG = 6; ES/RJ = 7; SP = 8; PR/SC = 9; RS = 0) — a lib JS expõe `getCpfInfo()` com `fiscalRegion` e lista de UFs — [brazilian-utils `get-cpf-info` / `_internals/constants/cpf.ts`](https://github.com/brazilian-utils/javascript/tree/main/src/get-cpf-info) (mapa parcial lido no código: AC=2, AL=4, AP=2, AM=2, BA=5, CE=3, DF=1, ES=7, GO=1, MA=3, MT=1, MS=1, MG=6, PR=9, PB=4; demais UFs **[NÃO VERIFICADO nesta sessão, conhecimento prévio]**).
- Vetores testados localmente (implementação abaixo): `529.982.247-25` válido; `111.444.777-35` válido; `111.111.111-11` inválido (repetido) — execução local em 16/11/2026.
- O CPF passou a ser o **número único da nova Carteira de Identidade Nacional (CIN)**: Lei 7.116/1983 alterada pela Lei 14.534/2023 determina que órgãos de identificação usem o CPF como número de registro geral; quem não tem CPF recebe um no ato — [Jornal Contábil](https://www.jornalcontabil.com.br/noticia/85432/rg-e-cpf-se-tornam-documentos-unificados-e-sera-preciso-emitir-novo-documento); [Folha Vitória](https://www.folhavitoria.com.br/cotidiano/nova-identidade-quem-precisa-tirar-agora-e-quem-pode-esperar/)
- O CPF é classificado como **identificador direto** (identifica sozinho o titular) na minuta do Guia de Anonimização e Pseudonimização da ANPD (consulta pública jan–mar/2024) — [Mattos Filho](https://www.mattosfilho.com.br/unico/anonimizacao-pseudonimizacao-direitos-titulares/); [Cescon Barrieu](https://cesconbarrieu.com.br/anpd-abre-consulta-a-sociedade-sobre-proposta-de-guia-de-anonimizacao-e-pseudonimizacao-para-protecao-de-dados-pessoais/)
- Ferramentas comerciais de DLP já têm detectores de CPF (Microsoft Purview "Brazil CPF number", Palo Alto Enterprise DLP "National Id - Brazil - CPF", Delphix "Brazil CPF") — [Microsoft Learn](https://learn.microsoft.com/he-IL/purview/sit-defn-brazil-cpf-number); [Palo Alto](https://docs.paloaltonetworks.com/enterprise-dlp/reference/predefined-data-pattern-keywords/nationalid-brazil-cpf); [Delphix](https://help.delphix.com/cc/current/content/brazil_cpf.htm)

#### 1.2 CNPJ numérico e ALFANUMÉRICO (IN RFB 2.229/2024)
- **Estrutura alfanumérica:** 14 posições; raiz (pos. 1–8) e ordem/estabelecimento (pos. 9–12) podem combinar **letras maiúsculas e algarismos**; DVs (pos. 13–14) **sempre numéricos** — [Asaas](https://blog.asaas.com/cnpj-alfanumerico/); [Serpro](https://serpro.gov.br/menu/noticias/noticias-2024/cnpj-alfanumerico); [Receita Federal – Perguntas e Respostas CNPJ alfanumérico (PDF)](https://www.gov.br/receitafederal/pt-br/centrais-de-conteudo/publicacoes/perguntas-e-respostas/cnpj/cnpj-alfanumerico.pdf) (via snippet; fetch bloqueado).
  - Conflito: uma notícia sobre o primeiro CNPJ emitido diz que "a raiz continua só com algarismos" — [resumo de busca de notícias de 08/2026, ex. CRC-MA](https://crcma.org.br/noticias/primeiro-cnpj-alfanumerico-e-emitido-pela-receita-federal). Isso provavelmente reflete apenas o caso concreto (filial do Banco do Brasil, que mantém a raiz numérica `00.000.000` e recebeu ordem alfanumérica `E08G`), não a regra; a FAQ da Receita e Serpro dizem que a raiz também pode ser alfanumérica. **Validadores devem aceitar letras nas 12 primeiras posições.**
- **Cálculo do DV:** módulo 11 com os mesmos pesos do CNPJ numérico (DV1: `5,4,3,2,9,8,7,6,5,4,3,2`; DV2: `6,5,4,3,2,9,8,7,6,5,4,3,2`), mas cada caractere vale `ord(c) − 48` (A=17, B=18, … Z=42); resto 0 ou 1 → DV 0; senão `11 − resto` — [Tecnospeed](https://blog.tecnospeed.com.br/cnpj-alfanumerico/); [NFe.io](https://nfe.io/blog/financeiro/cnpj-tudo-sobre/); [e-Auditoria](https://www.e-auditoria.com.br/blog/cnpj-alfanumerico/); implementado assim em [validate-docbr CNPJ.py](https://github.com/alvarofpp/validate-docbr/blob/main/validate_docbr/CNPJ.py) e [brazilian-utils `_internals/constants/cnpj.ts`](https://github.com/brazilian-utils/javascript/tree/main/src/_internals/constants)
- **Exemplo oficial da Receita:** `12.ABC.345/01DE` → valores `1,2,17,18,19,3,4,5,0,1,20,21`; soma ponderada DV1 = 459; 459 % 11 = 8; DV1 = 3 — [Receita FAQ via snippet de busca](https://www.gov.br/receitafederal/pt-br/centrais-de-conteudo/publicacoes/perguntas-e-respostas/cnpj/cnpj-alfanumerico.pdf). **Verificado localmente:** soma 459 e DVs completos `35` → `12.ABC.345/01DE-35` é válido (execução local 16/11/2026).
- **Vigência e status:** novos CNPJs alfanuméricos a partir de julho/2026; o **primeiro foi gerado em 31/07/2026** para filial do Banco do Brasil: `00.000.000/E08G-12`; emissão gradual; CNPJs existentes **não mudam**; MEI deve seguir numérico inicialmente — [Agência Gov/EBC](https://agenciagov.ebc.com.br/noticias/202607/receita-federal-gera-o-primeiro-cnpj-em-formato-alfanumerico); [Fenacon](https://fenacon.org.br/noticias/primeiro-cnpj-alfanumerico-e-emitido-pela-receita-federal/); [Tecnoblog](https://tecnoblog.net/noticias/cnpj-com-letras-e-numeros-comeca-a-valer-veja-o-que-muda/); [Senior – Portal de Exigências Legais 03/08/2026](https://documentacao.senior.com.br/exigenciaslegais/noticias/federal/2026/2026-08-03-cnpj-alfa-receita-federal-gera-o-primeiro-cnpj-em-formato-alfanumerico). **Verificado localmente:** `00000000E08G12` passa no algoritmo ASCII−48 (DVs calculados = `12`), o que confirma o algoritmo com um número real.
- Nota técnica conjunta para documentos fiscais eletrônicos (NT 2025.001, 25/04/2025) trata da adaptação de NF-e/CT-e etc. ao CNPJ alfanumérico — [Portal SPED Brasil](https://portalspedbrasil.com.br/forum/df-es-nota-tecnica-conjunta-cnpj-alfanumerico-nota-tecnica-2025-001-versao-1-00-de-25-de-abril-de-2025/)
- **Armadilha de biblioteca:** em `@brazilian-utils/brazilian-utils` v2.5.0, `isValidCnpj(x)` **por padrão só aceita CNPJ numérico**; o alfanumérico exige `isValidCnpj(x, { version: 2 })` — [código `is-valid-cnpj.ts`](https://github.com/brazilian-utils/javascript/tree/main/src/is-valid-cnpj). Já `validate-docbr` 2.x aceita ambos automaticamente (normaliza para maiúsculas) e gera alfanumérico com `generate(digits_only=False)` — [validate-docbr CNPJ.py](https://github.com/alvarofpp/validate-docbr/blob/main/validate_docbr/CNPJ.py)
- CNPJ de pessoa jurídica em geral não é dado pessoal, mas é dado pessoal quando identifica pessoa natural (MEI/empresário individual cuja razão social contém o nome e às vezes o CPF) — **[inferência; ver seção Inferências]**.

#### 1.3 RG (registro geral estadual) e CIN
- RG antigo segue válido até **28/02/2032** (Decreto 10.977/2022); para pessoas com 60+ anos na data do decreto, validade indeterminada; a CIN usa o CPF como número — [Itatiaia](https://www.itatiaia.com.br/brasil/brasil-geral/ate-quando-vale-o-rg-antigo-veja-prazo-para-tirar-a-nova-carteira-de-identidade/); [Folha Vitória](https://www.folhavitoria.com.br/cotidiano/nova-identidade-quem-precisa-tirar-agora-e-quem-pode-esperar/). Conflito: um veículo menciona prazo de troca "2028→2032"; demais fontes tratam 2032 como fim da validade — [resumo da busca](https://www.jb.com.br/editorias/?p=379).
- Nenhuma das bibliotecas analisadas (validate-docbr, brutils-python, brazilian-utils JS) implementa validação de RG estadual — verificado pela listagem de módulos dos repositórios ([validate-docbr](https://github.com/alvarofpp/validate-docbr/tree/main/validate_docbr); [brutils-python](https://github.com/brazilian-utils/brutils-python/tree/main/brutils); [brazilian-utils JS src/](https://github.com/brazilian-utils/javascript/tree/main/src)).

#### 1.4 CNH (Registro Nacional de Carteira de Habilitação)
- 11 dígitos (9 base + 2 DV); máscara de formatação usada pela lib: `NNN NNN NNN NN`. Algoritmo implementado: DV1 = `Σ d[i]·(9−i)` (pesos 9..1) `% 11`; se ≥10 → 0 e "desconto" `dsc = 2`. DV2 = `(Σ d[i]·(i+1)` (pesos 1..9) `% 11) − dsc`; se <0 soma 11; se ≥10 → 0. Rejeita repetidos — [validate-docbr CNH.py](https://github.com/alvarofpp/validate-docbr/blob/main/validate_docbr/CNH.py)
- Também em brutils-python (`cnh.py`) e brazilian-utils JS (`is-valid-cnh`) — [brutils-python](https://github.com/brazilian-utils/brutils-python/tree/main/brutils); [brazilian-utils JS](https://github.com/brazilian-utils/javascript/tree/main/src)

#### 1.5 Título de Eleitor
- 12 dígitos: 8 sequenciais + 2 de UF (01–28; 01=SP, 02=MG, … 28=ZZ/exterior) + 2 DVs; DV1 = `Σ seq[i]·(2..9) % 11` (10 → 0); DV2 = `(uf[0]·7 + uf[1]·8 + DV1·9) % 11` (10 → 0); máscara de formatação `NNNN NNNN NNNN`; base normativa citada: Resolução TSE 23.659/2021, art. 36 — [validate-docbr TituloEleitoral.py](https://github.com/alvarofpp/validate-docbr/blob/main/validate_docbr/TituloEleitoral.py)
- **Conflito entre bibliotecas:** `brutils-python` aplica exceção para SP e MG (UF 01/02): se resto = 0, DV = 1 (em DV1 e DV2) — [brutils-python voter_id.py](https://github.com/brazilian-utils/brutils-python/blob/main/brutils/voter_id.py); `validate-docbr` **não** aplica, afirmando que essa ressalva não consta na Resolução (issue #70) — [validate-docbr TituloEleitoral.py](https://github.com/alvarofpp/validate-docbr/blob/main/validate_docbr/TituloEleitoral.py). Para detecção (não para emissão), recomenda-se aceitar **ambas** as variantes para não gerar falso negativo.
- O título de eleitor por si não é sensível, mas zona/seção e filiação partidária ligadas a ele revelam "opinião política"/filiação, que são dados sensíveis (ver seção 2).

#### 1.6 PIS/PASEP/NIT/NIS (mesmo algoritmo)
- 11 dígitos, máscara `NNN.NNNNN.NN-N`; pesos `3,2,9,8,7,6,5,4,3,2` nos 10 primeiros; resto <2 → 0, senão `11 − resto` — [validate-docbr PIS.py](https://github.com/alvarofpp/validate-docbr/blob/main/validate_docbr/PIS.py)

#### 1.7 CNS (Cartão Nacional de Saúde)
- 15 dígitos; máscara `NNN NNNN NNNN NNNN`; primeiro dígito ∈ {1,2} (definitivo, derivado do PIS) ou {7,8,9} (provisório). Para 7/8/9: `Σ d[i]·(15−i)` sobre os 15 dígitos deve ser `≡ 0 (mod 11)`. Para 1/2: pegar os 11 primeiros, `s = Σ d[i]·(15−i)`, `dv = 11 − s%11` (11→0); se dv=10: `s += 2`, `dv = 11 − s%11`, sufixo `"001"+dv`; senão sufixo `"000"+dv` — [validate-docbr CNS.py](https://github.com/alvarofpp/validate-docbr/blob/main/validate_docbr/CNS.py). Vetor `898 0012 3456 7891` passa (teste local).
- CNS é identificador do SUS e, por contexto, liga o titular a dados de saúde (ver seção 2).

#### 1.8 RENAVAM
- 11 dígitos (RENAVAMs antigos de 9 dígitos são completados com zeros à esquerda); pesos `3,2,9,8,7,6,5,4,3,2` nos 10 primeiros; DV = `(soma·10) % 11`, 10 → 0 — [validate-docbr RENAVAM.py](https://github.com/alvarofpp/validate-docbr/blob/main/validate_docbr/RENAVAM.py). `brdocs-validation` (Pydantic) aceita RENAVAM de 9, 10 e 11 dígitos — [PyPI brdocs-validation](https://pypi.org/project/brdocs-validation/)

#### 1.9 Placa de veículo
- Formato antigo `LLL-NNNN` (regex `^[A-Z]{3}[0-9]{4}$`) e Mercosul `LLLNLNN` (regex `^[A-Z]{3}[0-9][A-Z][0-9]{2}$`); a lib converte antiga→Mercosul trocando o 5º caractere (dígito 0–9 → letra A–J) — [brazilian-utils `is-valid-license-plate/constants.ts`](https://github.com/brazilian-utils/javascript/tree/main/src/is-valid-license-plate); [`convert-license-plate-to-mercosul`](https://github.com/brazilian-utils/javascript/tree/main/src/convert-license-plate-to-mercosul). Sem DV.

#### 1.10 CEP
- 8 dígitos `NNNNN-NNN`, sem DV; brazilian-utils tem `is-valid-cep`, `get-state-by-cep`, `get-address-info-by-cep` — [brazilian-utils src/](https://github.com/brazilian-utils/javascript/tree/main/src)

#### 1.11 Telefone
- Número nacional tem 10 (fixo) ou 11 (celular) dígitos; prefixos de país aceitos `55`/`0055`; celular: 3º dígito (após DDD) ∈ {7,8,9} na "versão 1"; versão 2 exclui prefixo satelital `700`; valida DDD contra lista dos 67 DDDs em uso (Plano Geral de Numeração) — [brazilian-utils `is-valid-mobile-phone`, `_internals/constants/phone.ts`, `area-codes.ts`](https://github.com/brazilian-utils/javascript/tree/main/src/is-valid-mobile-phone)

#### 1.12 Chaves PIX (DICT/BCB)
- Tipos atuais: CPF, CNPJ, telefone, e-mail, EVP (aleatória) — [BCB – DICT API 2.13.0_rc1](https://www.bcb.gov.br/content/estabilidadefinanceira/pix/api_dict_2.13.0_rc1.html)
- E-mail: máximo **77 caracteres**, minúsculo — [BCB DICT API](https://www.bcb.gov.br/content/estabilidadefinanceira/pix/api_dict_2.13.0_rc1.html); [Payzu docs](https://docs.payzu.com.br/docs/pix-processamento/endpoints/keys-and-dict/get_pix_key)
- Telefone: E.164 com `+55`, ex. `+5511999999999` — [EYT docs](https://docs-eyt.pages.dev/en/pix-bacen/endpoints/dict-pix); [Payzu](https://docs.payzu.com.br/docs/pix-processamento/pix-key-types.en)
- EVP: UUID (v4) gerado pelo DICT, formato `8-4-4-4-12` hexadecimal, ex. `b6295ee1-f054-47d1-9e90-ee57b74f60d9` — [Payzu](https://docs.payzu.com.br/llms.mdx/docs/en/pix-processamento/pix-key-types/content.md); [Mobile Time](https://www.mobiletime.com.br/?p=623994)
- Implementação de detecção de tipo (ordem: EVP → e-mail → CNPJ v2 → CPF → telefone celular): `EVP_REGEX = /^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$/i`; `PIX_EMAIL_REGEX` com max 77 — [brazilian-utils `_internals/detect-pix-key-type` e `constants/pix-key.ts`](https://github.com/brazilian-utils/javascript/tree/main/src/_internals). A lib também valida/decodifica payload "Pix Copia e Cola" (BR Code/EMV) via `is-valid-pix-payload`/`get-pix-payload-info` — [brazilian-utils src/](https://github.com/brazilian-utils/javascript/tree/main/src)
- Observação: o BR Code (QR estático/dinâmico) embute nome do recebedor, cidade e a chave — portanto um payload Pix colado em log é dado pessoal — **[inferência a partir da estrutura do payload; Manual de Padrões para Iniciação do Pix](https://www.bcb.gov.br/content/estabilidadefinanceira/pix/Regulamento_Pix/II_ManualdePadroesparaIniciacaodoPix.pdf) não lido na íntegra nesta sessão]**.

#### 1.13 Conta bancária / agência
- Não há padrão único: DV varia por banco. A lib JS `is-valid-bank-account` implementa regras por código COMPE: Banco do Brasil (mód. 11, DV 10 → "X"), Bradesco (mód. 11 peso máx. 7, DV 10 → "P"), Santander (pesos `9,7,3,1,0,0,9,7,1,3,1,9,7,3` sobre agência+"00"+conta, mód. 10), Banrisul, Caixa (conta de 12 dígitos, dois DVs), HSBC, Citibank, Nubank (Verhoeff) e outros; para vários bancos valida **apenas estrutura** (`STRUCTURE_ONLY_BANK_CODES`) — [brazilian-utils `is-valid-bank-account`](https://github.com/brazilian-utils/javascript/tree/main/src/is-valid-bank-account) (lista de códigos lida no código: 077, 085, 102, 136, 197, 208, 212, 290, 318, 323, 336, 380, 403, 623, 655, 707, 748, 756; mapeamento código→nome **[NÃO VERIFICADO]**).

#### 1.14 Boleto / linha digitável
- Linha digitável bancária: **47 dígitos**; código de barras: **44**; 3 campos com DV mód. 10 (posições 9, 20, 31 da linha) + DV geral mód. 11 na posição 4 do código de barras; moeda "9" = Real; arrecadação/convênio (iniciado por "8") tem tratamento próprio (48 dígitos) — [brazilian-utils `is-valid-boleto` e `_internals/constants/boleto.ts`](https://github.com/brazilian-utils/javascript/tree/main/src/is-valid-boleto)
- **Fator de vencimento** chegou a 9999 em 21/02/2025 e reiniciou em 1000 em 22/02/2025 (base 07/10/1997; Carta-Circular BCB 2.926/2000); os mantenedores notam que não acharam documento oficial FEBRABAN com o reset, usando manual Bradesco "Layout da Cobrança" v17 — [brazilian-utils `get-boleto-info/constants.ts`](https://github.com/brazilian-utils/javascript/tree/main/src/get-boleto-info)
- Boleto em si não identifica pessoa diretamente, mas o "nosso número"/campo livre pode ser vinculado a pagador (CPF/CNPJ no registro do boleto) — **[inferência]**.

#### 1.15 Cartão de crédito (PAN)
- 13–19 dígitos, validação Luhn; brazilian-utils tem `is-valid-credit-card` — [brazilian-utils src/](https://github.com/brazilian-utils/javascript/tree/main/src). Luhn verificado localmente com `4111111111111111`.

#### 1.16 Passaporte brasileiro
- Regex usado pelas libs: `^[A-Z]{2}[0-9]{6}$` (2 letras + 6 dígitos), sem DV — [brazilian-utils `is-valid-passport/constants.ts`](https://github.com/brazilian-utils/javascript/tree/main/src/is-valid-passport); [brutils-python passport.py](https://github.com/brazilian-utils/brutils-python/blob/main/brutils/passport.py)

#### 1.17 Certidão de nascimento/casamento/óbito (matrícula)
- 32 dígitos, máscara `NNNNNN.NN.NN.NNNN.N.NNNNN.NNN.NNNNNNN-DD` (CNS da serventia, acervo, tipo de serviço, ano, tipo de livro, livro, folha, termo, DVs); DVs mód. 11 com multiplicador cíclico iniciando em `32 − len` e voltando a 0 após 10; resto >9 → 1 — [validate-docbr Certidao.py](https://github.com/alvarofpp/validate-docbr/blob/main/validate_docbr/Certidao.py). Também `is-valid-certidao`/`get-certidao-info` em brazilian-utils JS — [src/](https://github.com/brazilian-utils/javascript/tree/main/src)
- A matrícula revela ano de registro e cartório (localização), e o tipo de certidão (óbito/casamento) — **[inferência da estrutura]**.

#### 1.18 CRM / OAB / outros conselhos
- Sem DV para CRM/OAB; regex usada: `^(\d{4,6})([A-Z]{2})$` (número + UF) para OAB e CRM; CRO, CRP (região 01–24 + 4–6 dígitos) e CRC (`UF + 6 dígitos + categoria O/P + DV`) também suportados — [brazilian-utils `is-valid-registro-profissional/constants.ts`](https://github.com/brazilian-utils/javascript/tree/main/src/is-valid-registro-profissional)
- CRM é público (consulta no portal do CFM) e identifica profissional; em contexto de prontuário/receita, liga paciente a médico/especialidade — **[inferência]**.

#### 1.19 Testes locais de regex de detecção (16/11/2026)
Testei em texto sintético as regexes propostas na seção Inferências. Resultados relevantes para falsos positivos: a regex de telefone casou com o CPF não formatado `52998224725` (DDD 52 + "9" + 8 dígitos); a regex de CNPJ alfanumérico não formatado casou com os últimos 14 dígitos de uma linha digitável de boleto (`84340000010000`); a regex de OAB sem tratamento de ponto truncou `OAB/SP 123.456` em `123` (corrigida abaixo) — execução local de `rx.py` em scratchpad.

### Inferences

**Implementação Python de referência (testada localmente contra os vetores citados):**

```python
import re

def _mod11_dv(values, weights):
    r = sum(v * w for v, w in zip(values, weights)) % 11
    return 0 if r < 2 else 11 - r

# CPF
def cpf_valido(s: str) -> bool:
    d = re.sub(r"\D", "", s)
    if len(d) != 11 or len(set(d)) == 1:
        return False
    v = [int(c) for c in d]
    return (_mod11_dv(v[:9], range(10, 1, -1)) == v[9]
            and _mod11_dv(v[:10], range(11, 1, -1)) == v[10])

# CNPJ numérico + alfanumérico (IN RFB 2.229/2024)
W1 = [5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2]
W2 = [6] + W1
def cnpj_valido(s: str) -> bool:
    d = re.sub(r"[^0-9A-Za-z]", "", s).upper()
    if not re.fullmatch(r"[0-9A-Z]{12}[0-9]{2}", d) or len(set(d)) == 1:
        return False
    v = [ord(c) - 48 for c in d]          # '0'..'9' -> 0..9, 'A'..'Z' -> 17..42
    return _mod11_dv(v[:12], W1) == v[12] and _mod11_dv(v[:13], W2) == v[13]
# cnpj_valido("12.ABC.345/01DE-35") -> True ; cnpj_valido("00.000.000/E08G-12") -> True

# PIS/PASEP/NIT/NIS
def pis_valido(s):
    d = re.sub(r"\D", "", s)
    if len(d) != 11 or len(set(d)) == 1: return False
    v = [int(c) for c in d]
    return _mod11_dv(v[:10], [3, 2, 9, 8, 7, 6, 5, 4, 3, 2]) == v[10]

# RENAVAM (zfill(11) para os antigos de 9 dígitos)
def renavam_valido(s):
    d = re.sub(r"\D", "", s).zfill(11)
    if len(d) != 11: return False
    soma = sum(int(c) * w for c, w in zip(d[:10], [3, 2, 9, 8, 7, 6, 5, 4, 3, 2]))
    dv = (soma * 10) % 11
    return (0 if dv == 10 else dv) == int(d[10])

# CNS
def cns_valido(s):
    d = re.sub(r"\D", "", s)
    if len(d) != 15 or d[0] not in "12789": return False
    if d[0] in "12":
        base = d[:11]
        soma = sum(int(c) * (15 - i) for i, c in enumerate(base))
        dv = 11 - soma % 11
        dv = 0 if dv == 11 else dv
        if dv == 10:
            soma += 2; dv = 11 - soma % 11
            return d == base + "001" + str(dv)
        return d == base + "000" + str(dv)
    return sum(int(c) * (15 - i) for i, c in enumerate(d)) % 11 == 0

# Título de eleitor (aceita as duas variantes para SP/MG, para não perder detecção)
def titulo_valido(s):
    d = [int(c) for c in re.sub(r"\D", "", s)]
    if len(d) != 12: return False
    uf = d[8] * 10 + d[9]
    if not 1 <= uf <= 28: return False
    r1 = sum(a * b for a, b in zip(d[:8], range(2, 10))) % 11
    for spmg_exc in (False, True):
        dv1 = 0 if r1 == 10 else (1 if (spmg_exc and r1 == 0 and uf in (1, 2)) else r1)
        r2 = (d[8] * 7 + d[9] * 8 + dv1 * 9) % 11
        dv2 = 0 if r2 == 10 else (1 if (spmg_exc and r2 == 0 and uf in (1, 2)) else r2)
        if (dv1, dv2) == (d[10], d[11]): return True
    return False

# CNH
def cnh_valida(s):
    d = re.sub(r"\D", "", s)
    if len(d) != 11 or len(set(d)) == 1: return False
    v = [int(c) for c in d]
    dv1 = sum(v[i] * (9 - i) for i in range(9)) % 11
    dsc = 0
    if dv1 >= 10: dv1, dsc = 0, 2
    dv2 = sum(v[i] * (i + 1) for i in range(9)) % 11 - dsc
    if dv2 < 0: dv2 += 11
    if dv2 >= 10: dv2 = 0
    return dv1 == v[9] and dv2 == v[10]

# Luhn (cartões)
def luhn(s):
    ds = [int(c) for c in re.sub(r"\D", "", s)][::-1]
    return sum(d if i % 2 == 0 else (d * 2 - 9 if d * 2 > 9 else d * 2)
               for i, d in enumerate(ds)) % 10 == 0
```

**Regex de detecção sugeridas (testadas em amostra; usar sempre + validação DV + contexto):**

| Identificador | Formatado | Não formatado / tolerante | Principais falsos positivos |
|---|---|---|---|
| CPF | `(?<!\d)\d{3}\.\d{3}\.\d{3}-\d{2}(?!\d)` | `(?<![\d./-])\d{3}\.?\d{3}\.?\d{3}-?\d{2}(?![\d./-])` | PIS/NIT, CNH, RENAVAM, telefone celular com DDD (11 dígitos), timestamps, IDs sequenciais; ~1/100 números aleatórios de 11 dígitos passam no DV |
| CNPJ (num+alfa) | `[0-9A-Z]{2}\.[0-9A-Z]{3}\.[0-9A-Z]{3}/[0-9A-Z]{4}-\d{2}` | `(?<![0-9A-Za-z])[0-9A-Z]{2}\.?[0-9A-Z]{3}\.?[0-9A-Z]{3}/?[0-9A-Z]{4}-?\d{2}(?![0-9A-Za-z])` | Trechos de linha digitável/código de barras, chaves NF-e (44 díg.), hashes/IDs alfanuméricos em maiúsculas (base64/base32, códigos de produto). Sem máscara, **exigir palavra-chave** ("CNPJ", "inscrição") |
| PIS/NIT | `\d{3}\.\d{5}\.\d{2}-\d` | `\d{11}` | mesmo conjunto de 11 dígitos |
| CNS | `[12789]\d{2} \d{4} \d{4} \d{4}` | `(?<!\d)[12789]\d{14}(?!\d)` | números de pedido/protocolo de 15 dígitos, IMEI (15 dígitos, Luhn) |
| Título | `\d{4} \d{4} \d{4}` | `\d{12}` + UF 01–28 | quaisquer 12 dígitos |
| CNH | `\d{3} \d{3} \d{3} \d{2}` (formato da lib) | `\d{11}` | idem CPF |
| RENAVAM | `\d{10}-\d` | `\d{9,11}` | idem |
| Placa | `[A-Z]{3}-\d{4}` / `[A-Z]{3}\d[A-Z]\d{2}` | `(?<![A-Za-z0-9])[A-Z]{3}-?\d[A-Z0-9]\d{2}(?![A-Za-z0-9])` | códigos de produto/SKU, códigos de voo/aeroporto+número |
| CEP | `\d{5}-\d{3}` | `\d{8}` (só com contexto) | datas `AAAAMMDD`, números de 8 dígitos |
| Telefone | `(?<!\d)(?:\+?55[\s-]?)?\(?[1-9]{2}\)?[\s-]?(?:9\d{4}\|[2-5]\d{3})[\s-]?\d{4}(?!\d)` | — | CPF não formatado (testado), CNPJ parcial; DDDs brasileiros não contêm dígito 0 (por isso `[1-9]{2}`) **[NÃO VERIFICADO oficialmente; consistente com a lista de 67 DDDs da lib]** |
| PIX EVP | `(?i)\b[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}\b` | — | qualquer UUID (IDs de banco de dados, trace IDs) — só tratar como PIX com contexto ("chave", "pix") |
| Boleto | `\d{5}\.\d{5} \d{5}\.\d{6} \d{5}\.\d{6} \d \d{14}` | `\d{47}` / `\d{48}` / `\d{44}` | chaves de NF-e (44 dígitos) |
| Cartão | `(?<!\d)(?:\d[ -]?){12,18}\d(?!\d)` + Luhn | — | IMEI (Luhn), números de rastreio |
| Passaporte | `\b[A-Z]{2}\d{6}\b` | — | códigos genéricos (`AB123456`) — só com contexto |
| Certidão | `\d{6}\.\d{2}\.\d{2}\.\d{4}\.\d\.\d{5}\.\d{3}\.\d{7}-\d{2}` | `\d{32}` | hashes MD5 decimais raros; IDs longos |
| CRM | `\bCRM[\s/-]?[A-Z]{2}[\s/-]?\d{4,6}\b\|\bCRM[\s:]*\d{4,6}[\s/-]?[A-Z]{2}\b` | — | baixo (prefixo explícito) |
| OAB | `\bOAB[\s/-]?[A-Z]{2}[\s/-]?\d{1,3}(?:\.?\d{3})?(?:-?[A-Z])?\b` | — | baixo |

- **Probabilidade de falso positivo por DV:** dois DVs mód. 11 deixam passar ~1% de sequências aleatórias de 11 dígitos (1 em ~100); CNS com mód. 11 único ~1/11 para os provisórios (7/8/9). Logo, em varredura de logs, combinar com palavras-chave em janela (ex. ±40 caracteres: "cpf", "cnpj", "pis", "nit", "nis", "cns", "sus", "renavam", "título", "eleitor", "cnh", "habilitação", "placa", "cep", "pix", "chave") e reduzir score sem contexto — padrão idêntico ao do `PatternRecognizer` do Presidio com `context` words.
- **Um mesmo número pode passar em vários algoritmos** (ex.: um CPF válido pode também passar no DV de PIS ou CNH); classificar pela máscara e pelo contexto; se ambíguo, tratar como o mais restritivo (mascarar).
- **CNPJ alfanumérico — regras práticas:** normalizar para maiúsculas antes do DV (a Receita prevê só maiúsculas; libs fazem `upper()`), aceitar letras nas posições 1–12, exigir dígitos em 13–14, rejeitar todos iguais; campos de banco de dados `CHAR(14)`/`VARCHAR(18)` alfanuméricos (não `BIGINT`); **não** remover zeros à esquerda; ordenação/índices passam a ser lexicográficos.
- **Mascaramento convencional (exibição):**
  - CPF: `***.456.789-**` (mostra dígitos 4–9) — padrão amplamente usado em publicações oficiais (Portal da Transparência, Diários Oficiais) **[NÃO VERIFICADO nesta sessão a norma que o institui; ver Gaps]**. Alternativas comuns: `***.***.789-25` ou só últimos 2/3.
  - CNPJ: normalmente não mascarado (público); se for de empresário individual/MEI, mascarar como CPF ou ocultar.
  - RG/CIN: `**.***.678-*`; CNH: `*******8901`/`***.***.**9-01`; Título: `**** **** 1234` (manter UF?: os dígitos 9–10 revelam a UF de inscrição); PIS: `***.*****.78-*`; CNS: `*** **** **** 1234` (ou ocultar por inteiro, dado o contexto de saúde).
  - Telefone: `(11) 9****-4321`; e-mail: `j***@d***.com`; cartão (PCI DSS): primeiros 6/8 e últimos 4 no máximo (`4111 11** **** 1111`) ou só últimos 4.
  - Chave PIX: o próprio app Pix/BCB exibe CPF da chave mascarado como `***.456.789-**` na confirmação de pagamento **[NÃO VERIFICADO nesta sessão]**; EVP pode ser exibida (é aleatória, mas continua sendo identificador indireto).
  - Placa: `ABC-1***`; CEP: `01310-***` (manter 5 primeiros = região/setor); conta: `****5-6`.
- **Regra de ouro para o skill:** mascaramento de exibição (manter 6 de 11 dígitos de CPF) **não é anonimização** — `***.456.789-**` reduz o espaço a 10^3 candidatos (5 dígitos ocultos, dos quais 2 são DVs determinados → apenas 1.000 bases possíveis; com DV para confirmar). Para logs, preferir tokenização/HMAC (seção 4).

### Gaps
- PDF oficial da Receita (Perguntas e Respostas CNPJ Alfanumérico) e texto da IN RFB 2.229/2024 não puderam ser abertos (host gov.br bloqueado); dados vieram de snippets e de bibliotecas. Não confirmei se a Receita exclui alguma letra (ex. I/O/Q/U) — nenhuma fonte encontrada menciona exclusão; as bibliotecas aceitam A–Z completo.
- Validação de RG estadual: não encontrei nas bibliotecas analisadas nem verifiquei fontes oficiais. Conhecimento prévio **[NÃO VERIFICADO]**: SP usa 8 dígitos + DV mód. 11 com pesos 2..9 e DV "X" para 10; RJ e outros estados têm formatos próprios ou sem DV; vários estados não publicam o algoritmo. Recomenda-se detectar RG apenas por contexto ("RG", "identidade", "SSP/XX") e não validar DV.
- Documento normativo que fixa a máscara `***.456.789-**` (atribuída na prática a orientações governamentais de 2019–2021 para publicação de atos com CPF) não foi localizado nesta sessão.
- Especificação oficial da regex de chaves no Manual Operacional do DICT (incluindo se o DICT já aceita CNPJ alfanumérico como chave) não foi lida; a lib JS aceita CNPJ v2 como chave.
- Algoritmo oficial do CNS (Ministério da Saúde/DATASUS) não foi lido diretamente; o descrito vem de validate-docbr (amplamente replicado).
- Algoritmo de CNH: há variantes publicadas (algumas incluem o DV1 no cálculo do DV2); usei a de validate-docbr; não verifiquei contra documento do SENATRAN.

---

## 2. Dados sensíveis por contexto vs. dados pessoais comuns

### Takeaway
Pela LGPD, nenhum identificador numérico é "sensível" em si — sensível é a **informação que ele revela no contexto** (saúde, biometria, opinião política, religião, origem racial/étnica, vida sexual, dado genético, filiação sindical/religiosa/política). Na prática, CNS + dados clínicos, biometria/foto facial da CIN/CNH, título + filiação partidária, e dados de crianças exigem o regime reforçado (art. 11 / art. 14).

### Cited Findings
- A minuta da ANPD classifica CPF e nome completo como identificadores diretos; hash, substituição e criptografia são técnicas de **pseudonimização** (não anonimização), e se a reversão é possível com meios próprios da organização, trata-se de mera pseudonimização (dado continua pessoal) — [Mattos Filho](https://www.mattosfilho.com.br/unico/anonimizacao-pseudonimizacao-direitos-titulares/); [Mayer Brown 02/2024](https://www.mayerbrown.com/pt/insights/publications/2024/02/anonymization-and-pseudonymization-anpd-kicks-off-public-consultation-on-preliminary-study); [ANPD – Nota técnica de abertura TS 01/2024](https://www.gov.br/anpd/pt-br/acesso-a-informacao/participacao-social/outras-acoes/ts-01-2024-nota-tenica-6-de-abertura.pdf/@@display-file/file)
- A ANPD recomenda que o processo de anonimização não seja totalmente automatizado, com verificação por especialista humano — [Confidata (resumo da minuta)](https://confidata.com.br/blog/anonimizacao-pseudonimizacao-dados)
- Definição legal de dado sensível (LGPD art. 5º, II): origem racial ou étnica, convicção religiosa, opinião política, filiação a sindicato ou a organização de caráter religioso, filosófico ou político, dado referente à saúde ou à vida sexual, dado genético ou biométrico, quando vinculado a pessoa natural — [Lei 13.709/2018 (Planalto)](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm) (texto legal conhecido; página não aberta nesta sessão).

### Inferences
Classificação sugerida para o skill:

| Identificador | Categoria padrão | Torna-se sensível / alto risco quando… |
|---|---|---|
| CPF, CIN/RG, CNH (nº), passaporte, título, PIS/NIT, certidão | Pessoal comum (identificador direto) | Combinado com dados de saúde, biometria, religião etc.; RG/CNH/CIN físicos contêm **foto e impressão digital (biometria = sensível)**; CNH contém foto e assinatura |
| NIS (CadÚnico/Bolsa Família) | Pessoal comum | Revela condição socioeconômica/vulnerabilidade (alto risco, não "sensível" legal) |
| **CNS (Cartão SUS)** | Pessoal comum por definição, mas **quase sempre em contexto de saúde** | Em prontuários, receitas, laudos, agendamentos, sistemas e-SUS/RNDS → dado de saúde (sensível, art. 11) |
| CRM + nome de paciente | — | Revela atendimento/especialidade (saúde) |
| Título de eleitor | Pessoal comum | Com filiação partidária/opinião política → sensível |
| Placa, RENAVAM | Pessoal (identificam proprietário via DETRAN) | Geolocalização/trajetos (alto risco) |
| CEP + número, telefone, e-mail, chave PIX | Pessoal comum | Telefone/e-mail/PIX são vetores de fraude; PIX ligado a CPF |
| Conta/agência, cartão, boleto | Pessoal (financeiro) – não "sensível" na LGPD, mas sigilo bancário (LC 105/2001) e PCI DSS | — |
| Biometria (face, digital, voz), DNA | **Sensível sempre** | — |
| Dados de crianças/adolescentes (certidão, CPF de menor) | Regime do art. 14 (melhor interesse) | sempre |

- CNPJ normalmente não é dado pessoal, exceto empresário individual/MEI (nome da pessoa na razão social).

### Gaps
- Não verifiquei nesta sessão se a versão final do Guia de Anonimização/Pseudonimização da ANPD foi publicada até nov/2026 (só a minuta de 2024 apareceu nas buscas).
- Não localizei orientação da ANPD específica sobre CNS ou sobre identificadores de saúde do SUS.

---

## 3. Bibliotecas e ferramentas existentes (qualidade e cobertura)

### Takeaway
Para validação, `validate-docbr` (Python) e `@brazilian-utils/brazilian-utils` (JS/TS, muito abrangente) e `brutils-python` estão ativos e atualizados para o CNPJ alfanumérico (out/2026). Para **detecção em texto**, não há suporte nativo a Brasil no Presidio (nenhum recognizer `BR_*` no main em 14/11/2026), nem regras de CPF/CNPJ no gitleaks/detect-secrets — o skill precisará fornecer recognizers/regras customizadas.

### Cited Findings
- **validate-docbr** v2.0.1 (commit 01/10/2026): classes `CPF`, `CNPJ` (numérico + alfanumérico automático), `CNH`, `CNS`, `PIS`, `TituloEleitoral`, `RENAVAM`, `Certidao`; métodos `validate`, `generate(mask=…)`, `mask`; utilitário `validate_docs` para vários tipos; Python ≥ 3.10 — [GitHub alvarofpp/validate-docbr](https://github.com/alvarofpp/validate-docbr); [Algolia DocSearch resumo](https://docsearch.algolia.com/mcp/docs/repo/alvarofpp/validate-docbr)
  - Observação de qualidade: `TituloEleitoral` não aplica a exceção SP/MG (documentado como decisão, issue #70); `generate` usa `random.sample` (não criptográfico — ok para testes).
- **@brazilian-utils/brazilian-utils** (JS/TS) v2.5.0 (commit 09/10/2026, Node ≥ 24): `isValidCpf`, `isValidCnpj` (alfanumérico só com `{version: 2}`), `isValidCnh`, `isValidCns`, `isValidPis`, `isValidVoterId`, `isValidRenavam`, `isValidLicensePlate`, `isValidCep`, `isValidPhone`/`isValidMobilePhone`/`isValidLandlinePhone`, `isValidPixKey` (+`getPixKeyInfo`), `isValidPixPayload`, `isValidBoleto` (+`parseBoleto`, `getBoletoInfo`), `isValidBankAccount`, `isValidCreditCard`, `isValidPassport`, `isValidCertidao`, `isValidRegistroProfissional` (OAB/CRM/CRO/CRP/CRC), `isValidNfeKey`, `isValidIe`, `isValidCei`, `isValidCaepf`, `isValidProcessoJuridico`, além de `format-*`, `parse-*`, `generate-*` — [GitHub brazilian-utils/javascript (src/)](https://github.com/brazilian-utils/javascript/tree/main/src)
- **brutils-python** v2.5.0 (commit 29/10/2026): módulos `cpf`, `cnpj`, `cnh`, `pis`, `renavam`, `voter_id`, `passport`, `license_plate`, `phone`, `cep`, `email`, `legal_process`, `legal_nature` etc.; título aplica exceção SP/MG — [GitHub brazilian-utils/brutils-python](https://github.com/brazilian-utils/brutils-python)
- **brdocs-validation**: tipos Pydantic v2 para documentos brasileiros (CNH, CNS, RENAVAM 9/10/11 dígitos, TE…) — [PyPI](https://pypi.org/project/brdocs-validation/)
- Outros ecossistemas: `paemuri/brdoc` (Go) — [GitHub](https://www.github.com/paemuri/brdoc); `geekcom/validator-docs` (PHP/Laravel) — [Packagist](https://packagist.org/packages/geekcom/validator-docs); `brazilian_utils` (Rust) — [docs.rs](https://docs.rs/crate/brazilian_utils/latest/source/README.md); `@br-validators/core` (npm) — [socket.dev](https://socket.dev/npm/package/@br-validators/core); detectores "Brazil" do projeto `wuming` — [taoq-ai wuming](https://taoq-ai.github.io/wuming/detectors/br) (não avaliado em profundidade).
- **Microsoft Presidio:** em `presidio-analyzer/presidio_analyzer/predefined_recognizers/country_specific/` (main, commit `fd78e97` de 14/11/2026) existem pastas para australia, canada, finland, germany, india, italy, korea, nigeria, philippines, poland, singapore, south_africa, spain, sweden, thai, turkey, uk, us — **não há Brasil**; `grep` por "cpf"/"brazil" em todo o analyzer só retornou `iban_patterns.py` (IBAN BR genérico). Recognizers de país são registrados em `conf/default_recognizers.yaml` com `country_code` — [GitHub microsoft/presidio](https://github.com/microsoft/presidio/tree/main/presidio-analyzer/presidio_analyzer/predefined_recognizers/country_specific). Uma página de terceiros indica que recognizers country-specific vêm desabilitados por padrão — [tessl registry](https://tessl.io/registry/tessl/pypi-presidio-analyzer/files/docs/predefined-recognizers.md).
- **gitleaks** e **detect-secrets (Yelp):** clones atuais não contêm regras/plugins para CPF ou CNPJ (grep vazio em `config/` e no código) — [gitleaks](https://github.com/gitleaks/gitleaks); [detect-secrets](https://github.com/Yelp/detect-secrets). Ambos focam em segredos (tokens/chaves); dados pessoais exigem regras custom (`[[rules]]` com `regex` + `keywords` no gitleaks; plugin `RegexBasedDetector` no detect-secrets).
- DLP comerciais com CPF/CNPJ: Microsoft Purview, Palo Alto Enterprise DLP, Delphix — [Microsoft Learn](https://learn.microsoft.com/he-IL/purview/sit-defn-brazil-cpf-number); [Palo Alto](https://docs.paloaltonetworks.com/content/techdocs/en_US/enterprise-dlp/reference/predefined-data-pattern-keywords/nationalid-brazil-cpf.html); [Delphix BR Financial ID](https://help.delphix.com/dct/current/content/br_financial_id_framework.htm)

### Inferences
- **Presidio:** criar `PatternRecognizer`s `BR_CPF`, `BR_CNPJ`, `BR_CNS`, `BR_PIS`, `BR_TITULO`, `BR_CNH`, `BR_RENAVAM`, `BR_PLACA`, `BR_CEP`, `BR_TELEFONE`, `BR_PIX_EVP` com `supported_language="pt"`, `context=[...]` e `validate_result()` chamando os DVs acima (o Presidio aumenta/diminui score via validação e contexto). Para NER de nomes/endereços em português, usar `SpacyNlpEngine` com modelo `pt_core_news_lg` (ou `_md`/`_sm`), cujas entidades são `PER`, `LOC`, `ORG`, `MISC` (treinado em WikiNER) — mapear `PER→PERSON`, `LOC→LOCATION` **[NÃO VERIFICADO nesta sessão: versão atual e labels dos modelos spaCy pt; conhecimento prévio]**. Alternativas transformer para NER pt-BR (BERTimbau fine-tuned em LeNER-Br/HAREM) existem no Hugging Face **[NÃO VERIFICADO]**.
- **Regra gitleaks sugerida (CPF formatado, com validação manual posterior):**
  ```toml
  [[rules]]
  id = "br-cpf"
  description = "CPF brasileiro (dado pessoal - LGPD)"
  regex = '''(?i)(?:cpf|cadastro de pessoa)[^0-9]{0,20}(\d{3}\.?\d{3}\.?\d{3}-?\d{2})'''
  secretGroup = 1
  keywords = ["cpf"]
  [[rules]]
  id = "br-cnpj-alfanumerico"
  regex = '''(?i)cnpj[^0-9A-Z]{0,20}([0-9A-Z]{2}\.?[0-9A-Z]{3}\.?[0-9A-Z]{3}/?[0-9A-Z]{4}-?\d{2})'''
  secretGroup = 1
  keywords = ["cnpj"]
  ```
  gitleaks não valida DV nativamente → pós-filtrar com script; em fixtures de teste, usar números gerados (`validate-docbr.generate()`) e allowlist.
- Não identifiquei, nesta sessão, scanner "LGPD" open-source maduro e mantido no GitHub; o caminho mais robusto é Presidio + recognizers BR customizados.

### Gaps
- Não foi possível abrir a página oficial "supported entities" do Presidio (host bloqueado) nem verificar PRs abertos com recognizers brasileiros.
- Não pesquisei repositórios GitHub de "LGPD scanner" específicos (limite de chamadas); qualidade de projetos como `wuming` não avaliada.
- Versões atuais dos modelos spaCy pt e suas métricas não verificadas.

---

## 4. Técnicas: tokenização com preservação de formato, hash com sal/pepper, pseudonimização

### Takeaway
Hash simples (SHA-256/MD5) de CPF **não protege**: só existem 10^9 bases (os 2 DVs são determinísticos), e mesmo em Python single-core puro um ataque exaustivo leva ~10 min; em GPU, segundos. Use **HMAC-SHA-256 com chave secreta (pepper) guardada em KMS/HSM** para pseudônimos determinísticos (joins), ou **tokenização em cofre / FPE (NIST FF1)** quando o formato precisa ser preservado — e trate o resultado como dado pessoal pseudonimizado (LGPD art. 12/13), não anonimizado.

### Cited Findings
- Espaço do CPF: 9 dígitos de base + 2 DVs calculados → 10^9 CPFs possíveis — derivado do algoritmo em [validate-docbr CPF.py](https://github.com/alvarofpp/validate-docbr/blob/main/validate_docbr/CPF.py). Se a UF é conhecida, o 9º dígito (região fiscal) cai para 10^8 — [brazilian-utils `get-cpf-info`](https://github.com/brazilian-utils/javascript/tree/main/src/get-cpf-info).
- **Medição local (16/11/2026):** SHA-256 em Python puro, 1 núcleo: ~1,68 milhão hashes/s → 10^9 bases em **~9,9 minutos** (script `verify.py` no scratchpad). Hardware de GPU com hashcat é várias ordens de grandeza mais rápido **[valores de GPU NÃO VERIFICADOS nesta sessão]**.
- Uma fonte técnica sobre a minuta da ANPD recomenda sal para mitigar força bruta em CPFs porque o espaço é pequeno — [Confidata](https://confidata.com.br/blog/anonimizacao-pseudonimizacao-dados); a ANPD trata hash como pseudonimização — [Mattos Filho](https://www.mattosfilho.com.br/unico/anonimizacao-pseudonimizacao-direitos-titulares/)
- ANPD: anonimização sempre tem risco residual de reidentificação — [Mattos Filho](https://www.mattosfilho.com.br/?p=101268)

### Inferences
- **Sal aleatório por registro** impede correlação/joins e não impede força bruta direcionada (sal está ao lado do hash; 10^9 por registro continua barato). **Pepper/chave secreta** (HMAC) é o que realmente impede o ataque, desde que a chave fique fora do banco (KMS/HSM/Vault) e seja rotacionável (versão da chave no token, ex. `v2:hmac…`).
- Padrão recomendado para o skill:
  ```python
  import hmac, hashlib, re
  def pseudonimizar_cpf(cpf: str, chave: bytes, contexto: bytes = b"cpf:v1") -> str:
      d = re.sub(r"\D", "", cpf)            # normalizar ANTES (com/sem máscara geram o mesmo token)
      return hmac.new(chave, contexto + b":" + d.encode(), hashlib.sha256).hexdigest()
  ```
  - Para busca/indexação de igualdade: HMAC determinístico (como acima) em coluna separada ("blind index"), com o valor real criptografado (AES-GCM, envelope encryption) em outra coluna.
  - Para armazenamento que precisa recuperar o valor: tokenização com cofre (token aleatório ↔ valor em vault com controle de acesso) ou criptografia reversível; FPE (NIST SP 800-38G FF1; FF3-1 foi revisada/retirada **[status NÃO VERIFICADO]**) quando o sistema legado exige 11 dígitos — gerar token que **não passe** no DV (ou use prefixo reservado) para não ser confundido com CPF real.
  - Para ambientes de teste: usar geradores (`validate-docbr .generate()`, `@brazilian-utils generateCpf/generateCnpj`) em vez de cópia de produção.
  - Para KDF lenta (bcrypt/Argon2) em CPF: aumenta custo, mas com 10^9 candidatos e sal conhecido ainda é factível para alvo específico; preferir HMAC com segredo.
  - Logs: mascarar na borda (logger filter/middleware) usando os detectores da seção 1; nunca logar payload Pix copia-e-cola, linha digitável com dados do pagador, ou PAN.
  - k-anonimato/generalização para dados analíticos: CEP → 5 primeiros dígitos ou município; data de nascimento → ano/faixa etária; CNS/CPF → removidos ou HMAC com chave descartada (aproxima anonimização se nenhuma parte retém a chave).
- Mascaramento parcial de exibição (`***.456.789-**`) **não** é técnica de proteção para dados em repouso: com DV conhecido, sobra 10^3 candidatos.

### Gaps
- Não encontrei nesta sessão texto oficial da ANPD com recomendação específica de HMAC/pepper para CPF; recomendação baseada em boas práticas criptográficas.
- Não verifiquei status atual (nov/2026) do NIST SP 800-38G Rev.1 (FF3-1).
- Não medi taxa de hash em GPU.
