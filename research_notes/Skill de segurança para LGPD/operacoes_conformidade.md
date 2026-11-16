# Artefatos e fluxos operacionais de conformidade com a LGPD (RIPD, ROPA, LIA, consentimento, cookies, aviso de privacidade, direitos dos titulares, incidentes, encarregado, contratos/TID)

> Nota metodológica (pesquisa em 16/11/2026): nesta sessão, o WebFetch foi bloqueado pela rede para gov.br, in.gov.br, tce.pb.gov.br, confidata.com.br e outros. As fontes oficiais (gov.br/anpd, DOU) **não puderam ser abertas na íntegra**. Os achados vêm de resultados do WebSearch (resumos de escritórios de advocacia, Legismap, Migalhas, IAPP-like blogs) e de links para documentos oficiais que apareceram nas buscas. Os trechos marcados **[texto legal]** reproduzem o conteúdo da Lei 13.709/2018 (LGPD), cuja URL canônica é https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709compilado.htm. Esse texto não foi baixado de novo nesta sessão. Os itens marcados **[conhecimento prévio – verificar]** vêm de conhecimento anterior do pesquisador e não foram confirmados por fonte nesta sessão; o redator deve tratá-los como pendentes de checagem no texto oficial.

## 1. RIPD (art. 5º XVII, art. 38): quando é exigido, orientações e modelo da ANPD, seções obrigatórias

### Takeaway
Não existe ainda (nov/2026) regulamento da ANPD sobre o RIPD. Valem o art. 38 da LGPD (conteúdo mínimo: tipos de dados, metodologia de coleta e de segurança, análise de medidas/salvaguardas/mitigação), as "Perguntas e Respostas sobre o RIPD" da ANPD (06/04/2023, 15 perguntas) e, como modelo prático, o Modelo de RIPD v1.0 e o Guia do PPSI 2.0 do governo federal (SGD/MGI, 31/07/2026). O relatório é recomendado sempre que o tratamento puder gerar alto risco. Ele é exigível quando a ANPD o solicitar e nas hipóteses legais (ex.: art. 10 §3º, legítimo interesse; art. 4º §3º, segurança pública).

### Cited Findings
- A ANPD publicou em 06/04/2023 uma página com 15 perguntas e respostas sobre o RIPD, para orientar a sociedade enquanto o tema "ainda será regulamentado pela Autoridade" — [Legismap, notícias ANPD 06/04/2023](https://legismap.com.br/conteudos/artigos-e-noticias/noticias-anpd-em-06-04-2023); [Portal DORI](https://portaldori.com.br/2023/04/11/anpd-divulga-pagina-com-perguntas-e-respostas-sobre-o-relatorio-de-impacto-a-protecao-de-dados-pessoais-ripd/); [BMA](https://www.bmalaw.com.br/conteudo/direito-digital-protecao-de-dados-e-cybersecurity/artigos-e-noticias/anpd-divulga-perguntas-e-respostas-sobre-o-relatorio-de-impacto-a-protecao-de-dados-pessoais/pdf)
- As orientações da ANPD tratam de critérios e metodologia de elaboração e de conteúdo mínimo. A ANPD recomenda revisão contínua do RIPD, em especial quando fatos novos alterarem os riscos — [Mattos Filho](https://www.mattosfilho.com.br/unico/anpd-relatorio-protecao-dados-pessoais/)
- Enquanto não houver regulamento próprio, a ANPD indicou que se pode usar a definição de alto risco do art. 5º, XVII. A elaboração é "especialmente recomendável" quando o tratamento for capaz de gerar alto risco aos titulares — [Migalhas – ANPD esclarece dúvidas sobre o RIPD](https://www.migalhas.com.br/depeso/387026/anpd-esclarece-duvidas-sobre-o-relatorio-a-protecao-de-dados-pessoais); [Mayer Brown, 05/2023](https://www.mayerbrown.com/pt/insights/publications/2023/05/lgpd-e-os-esclarecimentos-sobre-o-ripd)
- Conteúdo mínimo (art. 38, parágrafo único): descrição dos tipos de dados coletados; metodologia usada para a coleta e para garantir a segurança das informações; análise do controlador sobre medidas, salvaguardas e mecanismos de mitigação de risco. A ANPD orienta que o documento seja detalhado o bastante para dar compreensão ampla do tratamento — [Confidata](https://confidata.com.br/blog/como-elaborar-ripd-lgpd); [BMA](https://www.bmalaw.com.br/conteudo/direito-digital-protecao-de-dados-e-cybersecurity/artigos-e-noticias/anpd-divulga-perguntas-e-respostas-sobre-o-relatorio-de-impacto-a-protecao-de-dados-pessoais/pdf)
- [texto legal] Art. 5º, XVII: RIPD é a "documentação do controlador que contém a descrição dos processos de tratamento de dados pessoais que podem gerar riscos às liberdades civis e aos direitos fundamentais, bem como medidas, salvaguardas e mecanismos de mitigação de risco". Art. 38: a ANPD "poderá determinar ao controlador que elabore" o RIPD, inclusive de dados sensíveis. Art. 10, §3º: a ANPD pode solicitar o RIPD quando o tratamento tiver como fundamento o legítimo interesse — [LGPD, Planalto](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709compilado.htm)
- Modelo prático oficial do Executivo federal: "Modelo de RIPD v1.0" e "Guia para elaboração de RIPDs v0.1", ambos datados de 31/07/2026, do Programa de Privacidade e Segurança da Informação (PPSI 2.0) da SGD/MGI. Eles referenciam as perguntas e respostas da ANPD e usam licença CC BY-NC-ND 4.0 — [Modelo de RIPD v1.0 (gov.br/governodigital)](https://www.gov.br/governodigital/pt-br/privacidade-e-seguranca/ppsi-2.0/arquivos/modelo-de-ripd-v1-0-31072026.pdf); [Guia para elaboração de RIPDs v0.1](https://www.gov.br/governodigital/pt-br/privacidade-e-seguranca/ppsi-2.0/arquivos/guia-para-elaboracao-de-ripds-v0-1-31072026.pdf)
- A ANPD **não aprovou** o Guia Orientativo sobre tratamento de dados de alto risco (art. 4º §3º da Res. 2/2022), por ser complexo para agentes de pequeno porte e ter foco limitado na gestão de riscos. A análise de alto risco pode ser feita por meio do RIPD, e a ANPD pretende tratar o alto risco junto com a regulamentação do RIPD — [Mattos Filho – ANPD não aprova guia de alto risco](https://www.mattosfilho.com.br/unico/anpd-guia-dados-risco/); [minuta pós-consulta (Telesíntese, 03/04/2024)](https://telesintese.com.br/wp-content/uploads/2024/04/20240403-versao-limpa-guia-alto-risco-apos-cp.pdf)
- Alto risco na Res. CD/ANPD 2/2022, art. 4º: exige pelo menos um critério geral (larga escala, ou tratamento que possa afetar significativamente interesses e direitos fundamentais) e pelo menos um critério específico — [Mattos Filho](https://www.mattosfilho.com.br/unico/anpd-guia-dados-risco/); [Res. 2/2022 (cópia gov.br/palmares)](https://www.gov.br/palmares/pt-br/midias/arquivos-menu-acesso-a-informacao/legislacao/resolucao-cd-anpd-n2-2022.pdf)
- As consultas públicas da ANPD em 2026 (CP 1/2026, fiscalização e processo sancionador, até 26/10/2026; CP 2/2026, processo regulatório, 06/10 a 23/11/2026; consulta sobre dosimetria, até 30/11/2026) não tratam do RIPD. Nenhuma consulta específica sobre RIPD foi localizada — [Teletime 09/09/2026](https://teletime.com.br/09/09/2026/anpd-consulta-fiscalizacao/); [ProcTracker CP 2/2026](https://proctracker.app/blog/anpd-consulta-publica-2-2026-processo-regulatorio-revisao-portaria-16)
- Sobre a CP 1/2026, um artigo sugere que registros documentais como o RIPD podem servir de evidência de boa-fé em defesa no processo sancionador — [HDPO](https://hdpo.com.br/anpd-regulamento-fiscalizacao-consulta-publica/)
- Há uma proposta acadêmica/profissional de atualização da diretriz metodológica do RIPD federal — [Migalhas 402619](https://www.migalhas.com.br/depeso/402619/diretriz-metodologica-para-elaboracao-do-ripd-proposta-de-atualizacao); [FGV Direito SP – comparação de metodologias de risco para RIPD](https://direitosp.fgv.br/sites/default/files/arquivos/analise-comparativa-de-metodologias-para-avaliacao-de-riscos-nos-processos-de-elaboracao-de-relatorios-de-impacto-a-protecao-de-dados-pessoais.pdf)

### Inferences
- Estrutura recomendada de RIPD para a skill, combinando o art. 38 com o modelo PPSI. [conhecimento prévio – verificar] O modelo federal anterior (SGD, 2020/2023) tinha estas seções; a v1.0 de 2026 provavelmente as mantém: (1) identificação dos agentes de tratamento e do encarregado; (2) necessidade de elaborar o relatório; (3) descrição do tratamento (natureza, escopo, contexto, finalidade); (4) partes interessadas consultadas; (5) necessidade e proporcionalidade (base legal, minimização, qualidade, transparência, direitos); (6) identificação e avaliação de riscos (probabilidade × impacto); (7) medidas para tratar os riscos (risco residual); (8) aprovação/assinaturas (controlador, encarregado). A skill deve gerar essas seções e marcar como obrigatórios os três itens do art. 38.
- Gatilhos sugeridos para a skill: alto risco (critério geral + específico da Res. 2/2022: tecnologias inovadoras/emergentes, vigilância ou controle de zonas acessíveis ao público, decisões exclusivamente automatizadas, dados sensíveis ou de crianças, adolescentes e idosos); fundamento em legítimo interesse; solicitação da ANPD; IA generativa treinada com dados pessoais.
- Para agentes de pequeno porte que realizem tratamento de alto risco, o regime simplificado (inclusive dispensa de encarregado) deixa de valer, e o RIPD se torna o instrumento natural de avaliação.

### Gaps
- O texto integral das 15 perguntas da ANPD (gov.br/anpd) não foi acessado. A lista exata de seções do Modelo de RIPD v1.0 (31/07/2026) não foi confirmada porque o PDF estava inacessível.
- Não foi confirmado se a regulamentação do RIPD continua na Agenda Regulatória 2025-2026 depois da alteração feita pela Res. CD/ANPD 31/2025, nem qual é seu prazo atual.

## 2. Registro das Operações de Tratamento (ROPA, art. 37): modelo simplificado da ANPD para pequeno porte e campos recomendados

### Takeaway
O art. 37 obriga controlador e operador a manter registro das operações, especialmente quando baseadas em legítimo interesse. A Res. CD/ANPD 2/2022 (art. 9º) permite registro simplificado para agentes de pequeno porte. A ANPD publicou o modelo em junho de 2023 (Excel e PDF), depois de tomada de subsídios (Nota Técnica 33/2022, 04/11/2022 a 03/01/2023). O modelo não é obrigatório e funciona como um "guia orientativo".

### Cited Findings
- A Res. CD/ANPD nº 2, de 27/01/2022 (regulamento para agentes de pequeno porte), prevê no art. 9º, parágrafo único, que a ANPD "fornecerá modelo para o registro simplificado" — [Mayer Brown 11/2022](https://www.mayerbrown.com/pt/insights/publications/2022/11/ropa-template-proposal-for-small-processing-agents); [Felsberg](https://www.felsberg.com.br/anpd-sugere-modelo-de-registro-de-atividades-de-tratamento-de-dados-para-agentes-de-tratamento-de-pequeno-porte-atpp/)
- Proposta inicial na Nota Técnica nº 33/2022, com tomada de subsídios de 04/11/2022 a 03/01/2023 (40 contribuições). O modelo final saiu em junho de 2023, em Excel e PDF — [Mattos Filho](https://www.mattosfilho.com.br/unico/anpd-subsidio-tratamento-dados/); [Legismap 14/06/2023](https://legismap.com.br/conteudos/artigos-e-noticias/noticias-anpd-em-14-06-2023); [Participa+Brasil – tomada de subsídios](https://www.gov.br/participamaisbrasil/tomada-de-subsidios-sobre-modelo-de-registro-de-atividades-de-tratamento-de-dados-pessoais-)
- O modelo é uma planilha com instruções, exemplos de preenchimento e colunas para registro. Contém "apenas os campos considerados essenciais" para a fiscalização. O voto do Conselho Diretor o descreve como "uma espécie de guia orientativo" que pode ser aprimorado pelas empresas, de uso não obrigatório — [Contábeis](https://www.contabeis.com.br/noticias/57454/anpd-simplifica-registro-de-dados-para-pequenas-empresas/); [Voto CD 14/2023](https://www.gov.br/anpd/pt-br/assuntos/deliberacoes-do-conselho-diretor-1/cds-ano-2023/cd-14-2023-votos.pdf)
- [texto legal] Art. 37: "O controlador e o operador devem manter registro das operações de tratamento de dados pessoais que realizarem, especialmente quando baseado no legítimo interesse." — [LGPD](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709compilado.htm)

### Inferences
- [conhecimento prévio – verificar] O modelo simplificado ANPD (jun/2023) organiza os campos aproximadamente assim: identificação do agente e do encarregado (ou canal de comunicação); nome ou descrição da operação/atividade; finalidade; hipótese legal; categorias de titulares; categorias de dados pessoais (com indicação de dados sensíveis); compartilhamento (com quem e para quê); transferência internacional (país); prazo ou critério de retenção; medidas de segurança. A skill pode adotá-lo como esquema mínimo e oferecer a versão completa (estilo GDPR art. 30 / Guia de Agentes de Tratamento) com campos extras: operadores envolvidos, fonte dos dados, sistemas, referências ao RIPD/LIA e responsável interno.
- Quando a base for legítimo interesse, o ROPA deve apontar para o teste de balanceamento (LIA), por causa do "especialmente" do art. 37 e do art. 10.

### Gaps
- A lista oficial exata de colunas da planilha da ANPD não foi verificada (gov.br inacessível).

## 3. Legítimo interesse: Guia Orientativo ANPD (fev/2024) e o teste de balanceamento em três fases

### Takeaway
O "Guia Orientativo – Hipóteses legais de tratamento de dados pessoais: Legítimo Interesse" foi publicado em 02/02/2024. Ele traz um modelo **não obrigatório** de teste de balanceamento em três fases: (i) finalidade, (ii) necessidade e (iii) balanceamento e salvaguardas. Se o resultado for inconclusivo ou se faltarem salvaguardas adequadas, outra base legal deve ser adotada. Um escritório entende que o guia cria, na prática, um dever de documentação.

### Cited Findings
- Publicado em 02/02/2024. O modelo de teste é dividido em "i) finalidade; ii) necessidade; e iii) balanceamento e salvaguardas", e não é de uso obrigatório — [Mattos Filho](https://www.mattosfilho.com.br/unico/anpd-legitimo-interesse-lgpd/); [Legismap](https://legismap.com.br/conteudos/artigos-e-noticias/anpd-lanca-guia-orientativo-sobre-legitimo-interesse)
- Se o resultado do balanceamento for inconclusivo, ou se não forem identificadas medidas de segurança e mitigação adequadas, outra base legal deve ser adotada — [Confidata – LIA](https://confidata.com.br/blog/legitimo-interesse-lgpd-lia-exemplos-limites)
- Há divergência sobre a obrigatoriedade: a ANPD exige que o agente demonstre a finalidade (teste de finalidade), e um escritório entende que o guia cria uma obrigação documental não prevista expressamente na lei — [Convergência Digital](https://convergenciadigital.com.br/governo/anpd-exige-teste-de-finalidade-para-tratamento-de-dados-por-legtimo-interesse); [BMA – O legítimo interesse na visão da ANPD](https://www.bmalaw.com.br/conteudo/direito-digital-protecao-de-dados-e-cybersecurity/artigos-e-noticias/o-legitimo-interesse-na-visao-da-anpd/pdf)
- Crianças e adolescentes: o guia admite legítimo interesse, desde que prevaleça o melhor interesse (art. 14) e o teste registre o que foi considerado melhor interesse — [Confidata](https://confidata.com.br/blog/lgpd-comentada-08-legitimo-interesse)
- O PDF do guia tem um anexo com modelo simplificado de teste (cópia hospedada no TCE-PB) — [guia_legitimo_interesse.pdf (TCE-PB)](https://tce.pb.gov.br/wp-content/uploads/2025/03/guia_legitimo_interesse.pdf)
- Voto do Conselho Diretor que aprovou o guia — [CD 05/2024 votos](https://www.gov.br/anpd/pt-br/assuntos/deliberacoes-do-conselho-diretor-1/circuitos-deliberativos-2024/cd-05-2024-votos.pdf)
- [texto legal] Art. 10: o legítimo interesse só fundamenta tratamento para finalidades legítimas, consideradas a partir de situações concretas (incluindo apoio e promoção de atividades do controlador e proteção do titular). §1º: somente dados estritamente necessários. §2º: o controlador adota medidas de transparência. §3º: a ANPD pode solicitar RIPD. Art. 7º, IX, ressalva os casos em que prevalecem direitos e liberdades fundamentais do titular. Dados sensíveis (art. 11) não admitem legítimo interesse — [LGPD](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709compilado.htm)

### Inferences
- Esqueleto de LIA para a skill:
  1. **Finalidade**: interesse legítimo, lícito e concreto (não especulativo), descrito em situação concreta; de quem é o interesse (controlador ou terceiro); está articulado com o ordenamento?
  2. **Necessidade**: os dados são estritamente necessários (minimização, art. 10 §1º)? Há meio menos intrusivo? Os dados são sensíveis (se sim, a base é vedada)?
  3. **Balanceamento e salvaguardas**: expectativas legítimas do titular; impacto em direitos e liberdades; titulares vulneráveis (crianças, com melhor interesse); medidas de transparência (art. 10 §2º); opt-out ou oposição (art. 18 §2º); salvaguardas de segurança; conclusão (prosseguir, prosseguir com mitigação, ou adotar outra base); registro no ROPA; reavaliação periódica.
- [conhecimento prévio – verificar] O guia de 2024 também aborda: legítimo interesse de terceiros; uso pelo Poder Público (em regra, não cabível para atividades típicas com prerrogativas estatais); e a recomendação de documentar o teste e disponibilizá-lo à ANPD quando requisitado.

### Gaps
- As perguntas literais de cada fase do anexo do guia não foram obtidas, porque o PDF estava inacessível.

## 4. Requisitos do consentimento (art. 8º e correlatos) e orientação da ANPD sobre bases legais

### Takeaway
O consentimento deve ser manifestação livre, informada e inequívoca para finalidade determinada (art. 5º XII). Deve ser por escrito ou outro meio que demonstre a vontade. Se escrito, deve ficar em cláusula destacada. O ônus da prova é do controlador. Autorizações genéricas são nulas. A revogação é gratuita e facilitada a qualquer momento. Para dados sensíveis, o consentimento deve ser "específico e destacado". Para crianças, deve ser específico e em destaque, dado por pelo menos um dos pais ou responsável. A ANPD não tem guia autônomo sobre consentimento. A matéria aparece no guia de cookies (2022), no guia de legítimo interesse (2024) e no Enunciado CD/ANPD 1/2023 (crianças).

### Cited Findings
- [texto legal] Art. 5º, XII: consentimento é "manifestação livre, informada e inequívoca pela qual o titular concorda com o tratamento de seus dados pessoais para uma finalidade determinada". Art. 8º: por escrito ou outro meio que demonstre a vontade (caput). Se por escrito, em cláusula destacada (§1º). Ônus da prova do controlador (§2º). Vedado com vício de consentimento (§3º). Finalidades determinadas, e autorizações genéricas são nulas (§4º). Revogável a qualquer momento por procedimento gratuito e facilitado (§5º). Em caso de alteração de finalidade, forma, duração, controlador ou compartilhamento, o titular deve ser informado e pode revogar (§6º e art. 9º §2º). Art. 11, I: dados sensíveis exigem consentimento "de forma específica e destacada, para finalidades específicas". Art. 14 §1º: crianças, consentimento específico e em destaque por pelo menos um dos pais ou responsável legal. Art. 9º §3º: se o consentimento for condição para o fornecimento de produto ou serviço, o titular deve ser informado com destaque — [LGPD](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709compilado.htm)
- A ANPD, já em documento de maio de 2022, recomendava o consentimento como principal base legal para cookies, com exceção dos estritamente necessários (que podem se apoiar em legítimo interesse) — resumo de busca referente a [BMA – recomendações ANPD sobre cookies no portal gov.br](https://www.bmalaw.com.br/conteudo/direito-digital-protecao-de-dados-e-cybersecurity/artigos-e-noticias/anpd-emite-recomendacoes-em-relacao-a-coleta-de-cookies-pelo-portal-govbr/pdf); [Ofício ANPD SEI 3368186](https://www.gov.br/anpd/pt-br/assuntos/noticias/sei_pr-3368186-oficio.pdf)

### Inferences
- Checklist de consentimento válido para a skill: granular por finalidade; sem caixas pré-marcadas; linguagem clara; identificação do controlador; registro de prova (timestamp, versão do texto, canal, identificador); mecanismo de revogação tão fácil quanto o de concessão; renovação quando houver mudança de finalidade; fluxo específico e destacado para dados sensíveis e para crianças, com verificação razoável do responsável (art. 14 §5º).
- [conhecimento prévio – verificar] O Enunciado CD/ANPD nº 1/2023 permite tratar dados de crianças e adolescentes com base em qualquer hipótese dos arts. 7º ou 11, desde que prevaleça o melhor interesse. O consentimento parental não é a única base.
- [conhecimento prévio – verificar] O "Guia Orientativo – Tratamento de dados pessoais pelo Poder Público" (2022, versão 2 em 2023) indica que o consentimento raramente é a base adequada para o setor público.

### Gaps
- Não foi localizado guia específico da ANPD sobre consentimento publicado em 2025-2026.
- O texto do Enunciado CD/ANPD 1/2023 não foi verificado nesta sessão.

## 5. Cookies: Guia Orientativo "Cookies e Proteção de Dados Pessoais" (ANPD, out/2022)

### Takeaway
O guia da ANPD (out/2022) organiza os cookies por categorias (necessários e não necessários, próprios e de terceiros, de sessão e persistentes, por finalidade: analíticos, de funcionalidade, de publicidade). Ele recomenda banner de primeiro nível com botão de rejeitar de fácil visualização e banner de segundo nível com categorias. Proíbe ou desaconselha cookies não necessários pré-ativados, destaque assimétrico do "aceitar" e ausência de segundo nível. O consentimento é a base principal para não necessários. Os estritamente necessários podem usar legítimo interesse.

### Cited Findings
- Guia publicado em 18/10/2022 — [Mattos Filho](https://www.mattosfilho.com.br/unico/anpd-guia-cookies-protecao-dados/); [Lefosse](https://lefosse.com/noticias/alerta/anpd-publica-guia-orientativo-sobre-o-uso-de-cookies/); [Souto Correa (EN)](https://www.soutocorrea.com.br/en/client-alerts/anpd-lanca-guia-orientativo-sobre-cookies-e-protecao-de-dados-pessoais/)
- Boa prática: "Disponibilizar botão que permita rejeitar todos os cookies não necessários, de fácil visualização, nos banners de primeiro e segundo nível". Prática não recomendada: "dificultar a visualização ou compreensão dos botões de rejeitar cookies" — [Felsberg](https://www.felsberg.com.br/cookies-e-protecao-de-dados-pessoais-orientacoes-da-anpd/); [Migalhas 376525](https://www.migalhas.com.br/depeso/376525/as-orientacoes-da-anpd-para-o-uso-de-cookies)
- Não recomendado: "apresentar cookies não necessários como já ativados por padrão" e "não disponibilizar banner de segundo nível". Boa prática: "classificar os cookies em categorias no banner de segundo nível" — [Felsberg](https://www.felsberg.com.br/cookies-e-protecao-de-dados-pessoais-orientacoes-da-anpd/); [BMA](https://www.bmalaw.com.br/conteudo/direito-digital-protecao-de-dados-e-cybersecurity/artigos-e-noticias/anpd-publica-guia-orientativo-sobre-cookies-e-protecao-de-dados-pessoais/pdf)
- Ativar cookies não necessários antes de qualquer interação com o banner é prática inválida — [Confidata – cookies](https://confidata.com.br/blog/cookies-rastreamento-consentimento-anpd)
- Classificação por finalidade (analíticos, de funcionalidade, de publicidade) e por outros critérios — [Legismap](https://legismap.com.br/conteudos/artigos-e-noticias/anpd-lanca-guia-orientativo-cookies-e-protecao-de-dados-pessoais)
- Um resultado de busca alega atualização do guia em janeiro de 2025. A alegação **não foi confirmada** por outra fonte — resumo de busca (fonte não identificada); tratar como não verificado.

### Inferences
- Checklist de banner para a skill:
  - 1º nível: aviso curto, botões "Aceitar todos", "Rejeitar não necessários" e "Configurar" com mesmo destaque visual, e link para a política de cookies.
  - 2º nível: categorias com toggles desligados por padrão (exceto necessários), descrição de finalidade, lista de terceiros e duração.
  - Não carregar scripts não necessários antes do opt-in.
  - Registrar o consentimento.
  - Oferecer meio permanente de revisão e revogação (ex.: link no rodapé).
  - Política de cookies com tabela: nome, provedor (próprio ou terceiro), finalidade, categoria, duração e base legal.
- [conhecimento prévio – verificar] O guia de 2022 também desaconselha o *cookie wall* (condicionar o acesso ao aceite de cookies não necessários), salvo justificativa, e recomenda não usar legítimo interesse para cookies de publicidade. O primeiro ponto não foi confirmado nesta sessão; os resultados não mencionam cookie wall.

### Gaps
- Confirmação textual sobre o *cookie wall* e sobre a suposta atualização de 2025.

## 6. Aviso/política de privacidade (art. 9º) e transparência

### Takeaway
O art. 9º lista as informações obrigatórias de acesso facilitado: finalidade específica, forma e duração, identificação e contato do controlador, uso compartilhado e sua finalidade, responsabilidades dos agentes e direitos do titular (com menção ao art. 18). O art. 41 §1º exige publicar identidade e contato do encarregado. A regulamentação do art. 9º faz parte do projeto de "direitos dos titulares" da Agenda 2025-2026, ainda não editado.

### Cited Findings
- [texto legal] Art. 9º: o titular tem direito ao acesso facilitado às informações sobre o tratamento, disponibilizadas de forma clara, adequada e ostensiva, sobre: I, finalidade específica; II, forma e duração; III, identificação do controlador; IV, informações de contato do controlador; V, uso compartilhado e finalidade; VI, responsabilidades dos agentes; VII, direitos do titular, com menção explícita aos do art. 18. Os §§1º e 2º tratam da nulidade do consentimento se as informações forem enganosas ou abusivas ou não forem apresentadas previamente, e da mudança de finalidade. O §3º trata do destaque quando o tratamento for condição para o serviço. Art. 6º, VI: princípio da transparência. Art. 10 §2º: transparência no legítimo interesse. Art. 14 §6º: informações sobre crianças em linguagem simples, considerando características físico-motoras, perceptivas, sensoriais, intelectuais e mentais, com uso de recursos audiovisuais quando adequado. Art. 41 §1º: identidade e informações de contato do encarregado divulgadas publicamente, de forma clara e objetiva, de preferência no sítio eletrônico do controlador — [LGPD](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709compilado.htm)
- O projeto de regulamentação dos direitos dos titulares na Agenda Regulatória 2025-2026 abrange os arts. 9º, 18, 19 e 20 (algumas fontes citam também o art. 23) — [Balanço da Agenda Regulatória 2025-2026, 2º sem./2025 (ANPD)](https://www.gov.br/anpd/pt-br/assuntos/regulacao/agenda-regulatoria-1/agenda-regulatoria-2025-2026/balanco-agenda-regulatoria-2025-2026-02-2025.pdf/@@display-file/file); [Machado Meyer – Agenda 2025-2026](https://www.machadomeyer.com.br/pt/inteligencia-juridica/publicacoes-ij/direito-digital/agenda-regulatoria-2025-2026-da-anpd-destaca-16-temas)
- Res. CD/ANPD 19/2024: uma lista de verificação cita a publicação das informações previstas no art. 17 do regulamento (transparência sobre transferência internacional) e a resposta aos titulares em 15 dias — [Lefosse](https://lefosse.com/noticias/transferencia-internacional-de-dados-prazo-para-adocao-das-clausulas-padrao-da-anpd-se-encerra-em-23-de-agosto/)

### Inferences
- Esqueleto de aviso de privacidade para a skill: controlador (razão social, CNPJ, contato); encarregado (nome ou PJ, canal); dados tratados por contexto; finalidades × base legal (tabela); compartilhamento (categorias de destinatários e finalidade); transferências internacionais (países ou mecanismo: adequação UE, Res. 32/2026, ou cláusulas-padrão da Res. 19/2024); retenção (prazo ou critério); direitos do art. 18 e como exercê-los (canal, prazo, verificação de identidade); segurança; cookies (link); crianças e adolescentes; decisões automatizadas (art. 20, direito de revisão); data de vigência e versionamento.
- Versão em camadas (resumo e texto completo) e linguagem simples são boas práticas coerentes com "clara, adequada e ostensiva".

### Gaps
- Não existe modelo oficial ANPD de aviso de privacidade. Nenhum foi localizado.

## 7. Requisições de titulares (arts. 18/19): fluxo, verificação de identidade, prazo de 15 dias, formatos e regulamentação 2025-2026

### Takeaway
Ainda não há regulamento da ANPD sobre direitos dos titulares (nov/2026). O projeto está na Agenda 2025-2026 (arts. 9º, 18, 19, 20), houve minuta em consulta com muitas contribuições, e ele não foi aprovado em 2025. A Res. CD/ANPD 30/2025 (Mapa de Temas Prioritários 2026-2027) colocou os direitos dos titulares como **primeiro tema prioritário de fiscalização**. Hoje valem o texto legal (resposta imediata simplificada ou declaração completa em até 15 dias, art. 19) e a regra de prazo em dobro para agentes de pequeno porte (Res. 2/2022).

### Cited Findings
- A Agenda Regulatória 2025-2026 (Res. CD/ANPD 23/2024) inclui a regulamentação dos direitos dos titulares (arts. 9º, 18, 19, 20 e, segundo algumas fontes, 23). A ANPD pretendia concluir o regulamento até o fim de 2025 — [Machado Meyer](https://www.machadomeyer.com.br/pt/inteligencia-juridica/publicacoes-ij/direito-digital/agenda-regulatoria-2025-2026-da-anpd-destaca-16-temas); [Balanço Agenda 2025-2026 (ANPD)](https://www.gov.br/anpd/pt-br/assuntos/regulacao/agenda-regulatoria-1/agenda-regulatoria-2025-2026/balanco-agenda-regulatoria-2025-2026-02-2025.pdf/@@display-file/file)
- Em 2025 só houve dois regulamentos no fim do ano: Res. CD/ANPD 31 (altera a Agenda Regulatória) e Res. CD/ANPD 30 (Mapa de Temas Prioritários 2026-2027). A minuta sobre direitos recebeu muitas contribuições que precisavam ser esclarecidas antes da aprovação — [Migalhas – Proteção de dados em 2025](https://www.migalhas.com.br/depeso/447221/protecao-de-dados-pessoais-em-2025-avancos-desafios-e-perspectivas); [Legismap – Res. CD/ANPD 31/2025](https://legismap.com.br/leis-e-normas/resolucao-cd-anpd-n-031-de-23-12-2025)
- A Res. CD/ANPD 30/2025 coloca os direitos dos titulares como primeiro dos quatro temas prioritários de fiscalização 2026-2027, ao lado de crianças e adolescentes no ambiente digital, setor público e IA — [Martinelli](https://www.martinelli.adv.br/anpd-publica-mapa-de-temas-prioritarios-2026-2027-e-atualiza-a-agenda-regulatoria-2025-2026/); [Embras](https://lgpd.embras.net/2025/12/29/anpd-publica-mapa-de-temas-prioritarios-para-o-bienio-2026-2027-e-atualiza-agenda-regulatoria-2025-2026/)
- Em 2026, a regulamentação dos arts. 9º, 18, 19 e 20 seguia em elaboração interna, sem data de aprovação — [Via Iuris](https://viaiuris.com.br/atualizacoes-da-anpd/); [LHLaw – ANPD em 2026](https://www.lhlaw.com.br/publicacoes/anpd-em-2026-principais-regulamentos-consultas-publicas-e-tendencias-2/)
- Minuta de resolução submetida à participação social ("Resolução CD/ANPD nº XX, de XX de dezembro de 2024"), disponível no Participa+Brasil. O conteúdo não foi verificado — [Participa+Brasil blob 57684](https://www.gov.br/participamaisbrasil/blob/baixar/57684)
- [texto legal] Art. 18: confirmação da existência de tratamento (I); acesso (II); correção (III); anonimização, bloqueio ou eliminação de dados desnecessários, excessivos ou ilícitos (IV); portabilidade (V, conforme regulamentação); eliminação dos dados tratados com consentimento (VI, ressalvado o art. 16); informação sobre compartilhamento (VII); informação sobre a possibilidade de não consentir e suas consequências (VIII); revogação do consentimento (IX). §2º: oposição a tratamento com dispensa de consentimento em caso de descumprimento. §3º: requerimento expresso do titular ou representante, ao agente de tratamento. §4º: se a providência não puder ser imediata, o controlador comunica que não é agente, indicando quem é, ou informa as razões de fato ou de direito. §5º: sem custos para o titular, nos prazos e termos do regulamento. §6º: comunicar aos agentes com quem os dados foram compartilhados a correção, eliminação, anonimização ou bloqueio. Art. 19: confirmação ou acesso em formato simplificado, imediatamente, ou por declaração clara e completa (origem, inexistência de registro, critérios utilizados e finalidade) em até 15 dias do requerimento. §1º: armazenamento em formato que favoreça o acesso. §2º: por meio eletrônico seguro ou impresso, à escolha do titular. §3º: quando o tratamento se basear em consentimento ou contrato, o titular pode solicitar cópia eletrônica integral em formato que permita reutilização. Art. 20: revisão de decisões automatizadas e informações sobre critérios, respeitados os segredos comercial e industrial. Art. 41 §2º, I: o encarregado aceita reclamações e comunicações dos titulares — [LGPD](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709compilado.htm)
- Agentes de pequeno porte têm prazos em dobro, inclusive para atender requisições de titulares, nos termos da Res. CD/ANPD 2/2022 — [BMA – Res. pequeno porte](https://www.bmalaw.com.br/conteudo/direito-digital-protecao-de-dados-e-cybersecurity/artigos-e-noticias/anpd-publica-resolucao-sobre-aplicacao-da-lgpd-para-agentes-de-tratamento-de-pequeno-porte/pdf) (confirmação do dobro para incidentes em [Mattos Filho](https://www.mattosfilho.com.br/unico/regulamento-incidente-seguranca/); para requisições [conhecimento prévio – verificar], art. 14 da Res. 2/2022)

### Inferences
- Fluxo de DSR para a skill:
  1. Recebimento por canal do encarregado, com protocolo e data.
  2. Verificação de identidade proporcional ao risco (não exigir mais dados do que o necessário; reaproveitar autenticação existente). A LGPD não detalha esse passo, e ele deve ser revisto quando houver regulamento.
  3. Classificação do direito (art. 18, I a IX, art. 20).
  4. Resposta simplificada imediata, ou declaração completa em até 15 dias (contagem corrida, salvo regulamento; 30 dias para pequeno porte se aplicável o dobro).
  5. Execução e propagação a terceiros (art. 18 §6º).
  6. Resposta por meio eletrônico seguro ou impresso, à escolha do titular.
  7. Negativa fundamentada (§4º).
  8. Registro e evidência.
  9. Encaminhamento de reclamação (art. 18 §1º: o titular pode peticionar à ANPD).
- Como os direitos são prioridade de fiscalização 2026-2027, a skill deve priorizar evidência de cumprimento: logs, SLA e modelos de resposta.

### Gaps
- Não se sabe se o regulamento de direitos foi aprovado entre o fim de 2025 e nov/2026. Nenhuma fonte encontrada indica aprovação, e o redator deve sinalizar como "pendente/verificar no DOU".
- Conteúdo da minuta (prazos detalhados, verificação de identidade, portabilidade) não verificado.

## 8. Resposta a incidentes: Res. CD/ANPD 15/2024 (Regulamento de Comunicação de Incidente de Segurança)

### Takeaway
A Res. CD/ANPD 15, de 24/04/2024 (DOU 26/04/2024), exige comunicar à ANPD e aos titulares, em **3 dias úteis** contados do conhecimento de que o incidente afetou dados pessoais, os incidentes que possam acarretar **risco ou dano relevante**. A comunicação à ANPD se faz por formulário eletrônico. Informações faltantes podem ser complementadas em 20 dias úteis. Agentes de pequeno porte têm prazo em dobro. Todos os incidentes, comunicados ou não, entram em registro mantido por no mínimo 5 anos. A norma substituiu a orientação anterior de "prazo razoável, em até 2 dias úteis".

### Cited Findings
- A comunicação à ANPD e aos titulares ocorre em 3 dias úteis contados do conhecimento, pelo controlador, de que o incidente afetou dados pessoais, por formulário eletrônico da ANPD — [Mattos Filho](https://www.mattosfilho.com.br/unico/regulamento-incidente-seguranca/); [Machado Meyer](https://www.machadomeyer.com.br/pt/inteligencia-juridica/publicacoes-ij/direito-digital/anpd-publica-regulamento-de-comunicacao-de-incidente-de-seguranca); [Cescon Barrieu](https://cesconbarrieu.com.br/anpd-aprova-o-regulamento-de-comunicacao-de-incidente-de-seguranca/)
- Segundo um escritório, o prazo corre a partir da ciência de que dados pessoais foram afetados, e não da conclusão da análise de risco — [Lefosse](https://lefosse.com/noticias/alerta/client-alert-anpd-aprova-regulamento-de-comunicacao-de-incidente-de-seguranca/); [Confidata](https://confidata.com.br/blog/comunicacao-incidente-seguranca-anpd)
- Complementação em 20 dias úteis contados da comunicação (art. 6º §3º). Prazos em dobro para agentes de pequeno porte (art. 6º §8º) — [Confidata](https://confidata.com.br/blog/comunicacao-incidente-seguranca-anpd); [Mattos Filho](https://www.mattosfilho.com.br/unico/regulamento-incidente-seguranca/)
- O conteúdo da comunicação inclui, entre outros itens, os riscos relacionados ao incidente com identificação dos possíveis impactos aos titulares, os motivos da demora (se fora do prazo) e as medidas adotadas ou a adotar para reverter ou mitigar os efeitos — [Global Suite Solutions](https://www.globalsuitesolutions.com/pt/?p=117761); [Mayer Brown 05/2024](https://www.mayerbrown.com/pt/insights/publications/2024/05/anpd-approves-data-breach-notifying-regulation)
- Comunicação aos titulares: depois de comunicá-los, o controlador tem 3 dias úteis contados do fim do prazo para declarar à ANPD que o fez, indicando os meios usados. A ANPD pode requisitar cópia do aviso — [Machado Meyer](https://www.machadomeyer.com.br/pt/inteligencia-juridica/publicacoes-ij/direito-digital/anpd-publica-regulamento-de-comunicacao-de-incidente-de-seguranca); [Tag DLaw](https://tagdlaw.com.br/anpd-comunicacao-de-incidentes-de-seguranca/)
- Registro: todos os incidentes, inclusive os não comunicados, devem ser registrados e mantidos por no mínimo 5 anos a partir do registro, salvo obrigação de prazo maior. A ANPD pode requisitá-los a qualquer tempo. O art. 10 §2º trata do setor público e das regras de guarda permanente — [Mattos Filho](https://www.mattosfilho.com.br/unico/regulamento-incidente-seguranca/); [CNB-SP – artigo sobre cartórios](https://cnbsp.org.br/2024/12/03/artigo-seguranca-da-informacao-em-cartorios-extrajudiciais-aspectos-praticos-da-comunicacao-e-registro-de-incidentes-com-dados-pessoais-por-daniel-ribeiro-dos-santos/)
- A orientação anterior da ANPD pedia comunicação em prazo razoável, não superior a 2 dias úteis da ciência. Essa orientação foi **superada** pela Res. 15/2024 — [Fórum CSIRTs 2024 – Opice Blum](https://forum.cert.br/forum2024/slides/forumcsirts2024-opiceblum.pdf); [AMDJUS](https://amdjus.com.br/anpd-determina-que-vazamento-de-dados-deve-ser-notificado-em-ate-3-dias/)
- Cópia do DOU da Res. 15/2024 — [SINTSE/TSE – DOU 26/04/2024](https://sintse.tse.jus.br/documentos/2024/Abr/26/diario-oficial-da-uniao-secao-1/autoridade-nacional-de-protecao-de-dados-resolucao-no-15-de-24-de-abril-de-2024-aprova-o-regulamento)
- Materiais práticos: "Boas práticas na comunicação de incidentes, 2ª ed." (Baptista Luz, maio/2024); webinário SGD sobre CIS (30/04/2025); protocolos de resposta de órgãos (PGFN, ICMBio); modelo de comunicação da EBC — [Baptista Luz](https://www.baptista.com.br/wp-content/uploads/2024/05/Boas-práticas-na-comunicação-de-incidentes_2ª-ed..pdf); [SGD – apresentação CIS 30/04/2025](https://www.gov.br/governodigital/pt-br/privacidade-e-seguranca/centro-de-excelencia-em-privacidade-e-seguranca/webnario/apresentacaocis-30abr2025-_final.pdf/@@download/file); [PGFN – protocolo](https://www.gov.br/pgfn/pt-br/acesso-a-informacao/privacidade-e-protecao-de-dados/pgfn-protocolorespincdadospessoais.pdf); [EBC – modelo de comunicação](https://www.ebc.com.br/lgpd/lgpd/modelo_de_comunicacao.pdf)

### Inferences
- [conhecimento prévio – verificar] Critérios do art. 5º da Res. 15/2024: o incidente pode acarretar risco ou dano relevante quando puder afetar significativamente interesses e direitos fundamentais dos titulares **e** envolver pelo menos um destes: (a) dados sensíveis; (b) dados de crianças, adolescentes ou idosos; (c) dados financeiros; (d) dados de autenticação em sistemas; (e) dados protegidos por sigilo legal, judicial ou profissional; (f) dados em larga escala. Os resultados desta sessão **não** confirmaram esses critérios, e eles devem ser checados no art. 5º.
- [conhecimento prévio – verificar] Itens do art. 6º (formulário ANPD): descrição da natureza e categoria dos dados afetados; número de titulares afetados (com crianças, adolescentes e idosos discriminados); medidas técnicas e de segurança antes e depois do incidente; riscos e possíveis impactos; motivos da demora; medidas para mitigar; data da ocorrência e da ciência; dados do encarregado ou representante; identificação do controlador (e se é pequeno porte); identificação do operador, quando aplicável; descrição do incidente e causa principal; total de titulares tratados na atividade afetada.
- [conhecimento prévio – verificar] Comunicação aos titulares (art. 9º): linguagem simples, de forma direta e individual quando possível (ou por meios amplos, se a identificação individual for inviável), com descrição dos dados afetados, riscos e consequências, medidas tomadas e recomendadas ao titular, data da ciência e contato do encarregado. Registro (art. 10): data da ciência, descrição geral, natureza e categoria dos dados, número de titulares, avaliação de risco, medidas de correção e mitigação, forma e conteúdo das comunicações e motivos para não comunicar.
- Playbook para a skill:
  - T0: detecção e contenção.
  - T0 + ≤1 dia útil: triagem ("afetou dados pessoais?"), que dispara a contagem de 3 dias úteis.
  - Avaliação de risco ou dano relevante (art. 5º).
  - Decisão documentada de comunicar ou não comunicar (o registro é obrigatório nos dois casos).
  - Comunicação preliminar à ANPD pelo formulário (D+3 úteis, ou D+6 para pequeno porte).
  - Aviso aos titulares (D+3 úteis) e declaração à ANPD.
  - Complementação (D+20 úteis da comunicação).
  - Lições aprendidas e atualização do RIPD/ROPA.
  - Guarda do registro por ≥5 anos.
  - O operador deve avisar o controlador sem demora, o que cabe prever em contrato.

### Gaps
- Texto literal dos arts. 5º, 6º, 9º e 10 e do formulário eletrônico atual da ANPD (sistema gov.br) não acessados.
- Não se sabe se a revisão do Regulamento de Fiscalização (CP 1/2026) altera algo do procedimento de incidentes.

## 9. Encarregado (DPO): Res. CD/ANPD 18/2024

### Takeaway
A Res. CD/ANPD 18, de 16/07/2024 (DOU 17/07/2024), regulamenta a atuação do encarregado. Ela trata de indicação por ato formal e documentado, divulgação de identidade e contato, atribuições, deveres do agente de tratamento e conflito de interesse. Pessoa natural ou jurídica pode exercer a função. É permitido acumular funções e atender mais de um agente, desde que sem conflito de interesse. O encarregado deve atuar com ética, integridade e autonomia técnica.

### Cited Findings
- Resolução nº 18 de 16/07/2024, publicada no DOU em 17/07/2024; aprova o Regulamento sobre a atuação do encarregado — [SINTSE/TSE – DOU 17/07/2024](https://sintse.tse.jus.br/documentos/2024/Jul/17/diario-oficial-da-uniao-secao-1/autoridade-nacional-de-protecao-de-dados-resolucao-no-18-de-16-de-julho-de-2024-aprova-o-regulamento); [cópia TJBA (PDF)](https://www.tjba.jus.br/extrajudicial/wp-content/uploads/2024/08/RESOLUCAO-ANPD-No-18-Encarregado-de-Dados.pdf)
- Conflito de interesse é a situação que possa comprometer, influenciar ou afetar de maneira imprópria a objetividade e o julgamento técnico. O encarregado pode acumular funções e atuar para mais de um agente se não houver conflito, e cabe ao agente evitar que o encarregado exerça atribuições conflitantes — [Migalhas 420330](https://www.migalhas.com.br/depeso/420330/conflito-de-interesses-na-funcao-de-dpo-segundo-a-resolucao-18-da-anpd); [Convergência Digital](https://convergenciadigital.com.br/internet/resolucao-da-anpd-e-o-conflito-de-interesses-na-funcao-de-dpo/); [Legismap](https://legismap.com.br/conteudos/artigos-e-noticias/conflito-de-interesse-na-atuacao-do-encarregado-pelo-tratamento-de-dados-pessoais)
- Ética, integridade e autonomia técnica (art. 18, segundo comentário). A nomeação deve ser formal e documentada. A pessoa jurídica é admitida expressamente — [Migalhas 412902](https://www.migalhas.com.br/depeso/412902/nova-regra-da-anpd-envolve-a-atuacao-do-encarregado-de-dados-pessoais); [CNB-SP (Brancher/Pfaltzgraff)](https://cnbsp.org.br/2024/08/09/artigo-nova-regra-da-anpd-envolvendo-a-atuacao-do-encarregado-de-dados-pessoais-por-paulo-marcos-rodrigues-brancher-e-maira-scala-pfaltzgraff/)
- As fontes divergem sobre a existência de sanções específicas para conflito de interesse: uma diz que a resolução não as detalha, outra afirma que prevê — [Migalhas 420330](https://www.migalhas.com.br/depeso/420330/conflito-de-interesses-na-funcao-de-dpo-segundo-a-resolucao-18-da-anpd); [Convergência Digital](https://convergenciadigital.com.br/internet/resolucao-da-anpd-e-o-conflito-de-interesses-na-funcao-de-dpo/)
- Agentes de pequeno porte são dispensados de indicar encarregado (Res. 2/2022), salvo se realizarem tratamento de alto risco. Nesse caso devem manter canal de comunicação — [Mattos Filho](https://www.mattosfilho.com.br/unico/anpd-guia-dados-risco/); [Confidata – pequeno porte](https://confidata.com.br/blog/lgpd-pequenas-empresas-resolucao-pequeno-porte)

### Inferences
- [conhecimento prévio – verificar] Pontos da Res. 18/2024 úteis à skill:
  - Ato formal de indicação, escrito, datado e assinado, com as formas de atuação e as atividades, apresentável à ANPD.
  - Divulgação no site em local de destaque e fácil acesso, com nome (pessoa natural, ou nome empresarial e responsável, se PJ) e contato que permita comunicação, inclusive com a ANPD. Em vez de canal, o operador pode atender por outros meios quando não houver site.
  - Não é exigida inscrição em entidade nem certificação.
  - Comunicação em português.
  - Substituto em ausências.
  - Atribuições: aceitar reclamações, receber comunicações da ANPD, orientar funcionários, além de assistir em registro de incidentes, ROPA, RIPD, mecanismos de autorregulação, transferências internacionais, regras de boas práticas e governança, contratos e Privacy by Design.
  - Agente de tratamento: prover recursos, autonomia técnica e acesso à alta administração. A responsabilidade continua sendo do agente, não do encarregado.
- Checklist de conflito: não acumular com funções que definem finalidades e meios do tratamento (ex.: diretor de TI ou marketing que decida tratamentos), avaliar caso a caso e documentar a análise.

### Gaps
- Texto literal dos artigos de atribuições, divulgação e conflito não acessado.

## 10. Contratos com operadores e cláusulas-padrão contratuais (Res. CD/ANPD 19/2024, Anexo II) e adequação UE (Res. 32/2026)

### Takeaway
A Res. CD/ANPD 19/2024 (Regulamento de Transferência Internacional de Dados, 23/08/2024) aprovou cláusulas-padrão contratuais (CPCs). Elas devem ser adotadas **integralmente e sem alterações**, e cláusulas específicas exigem aprovação prévia da ANPD. O prazo de 12 meses para incorporar as CPCs terminou em 23/08/2025. Uma retificação no DOU de 18/08/2025 alterou a cláusula 15.4(b). Desde a Res. CD/ANPD 32, de 26/01/2026, a UE é reconhecida como adequada, e transferências para lá dispensam CPCs. Os demais mecanismos continuam válidos. Para operadores domésticos, a LGPD não impõe cláusulas mínimas, mas os arts. 39, 42 e 46 e o Guia de Agentes de Tratamento orientam o conteúdo.

### Cited Findings
- A Res. 19/2024 deu 12 meses para quem usava cláusulas contratuais incorporar as CPCs. O período terminou em 23/08/2025 — [Lefosse](https://lefosse.com/noticias/transferencia-internacional-de-dados-prazo-para-adocao-das-clausulas-padrao-da-anpd-se-encerra-em-23-de-agosto/); [Mayer Brown 29/08/2025](https://www.mayerbrown.com/pt/insights/publications/2025/08/end-of-grace-period-implementation-of-brazils-standard-contractual-clauses-in-international-transfers-of-personal-data)
- As CPCs devem ser adotadas na íntegra e sem alterações. Cláusulas específicas dependem de aprovação prévia da ANPD — [Lefosse](https://lefosse.com/noticias/alerta/anpd-publica-regulamento-de-transferencia-internacional-de-dados-e-clausulas-padrao-contratuais-de-protecao-de-dados/); [Demarest](https://www.demarest.com.br/anpd-aprova-o-regulamento-de-transferencia-internacional-de-dados/); [Mattos Filho](https://www.mattosfilho.com.br/unico/regulamentacao-transferencia-internacional-dados/)
- A retificação no DOU de 18/08/2025 alterou a cláusula 15.4(b), que passou a remeter ao item 15.3. Versões copiadas antes dessa data devem ser conferidas — [Lex Legal](https://lexlegal.com.br/?p=32959); [Tozzini Freire – Cybernews 07/2025](https://tozzinifreire.com.br/site/conteudo/uploads/1-cybernews-0725-pt-68ac6ece4202f.pdf)
- Checklist de transparência: publicar as informações do art. 17 do regulamento e responder aos titulares em 15 dias — [Lefosse](https://lefosse.com/noticias/transferencia-internacional-de-dados-prazo-para-adocao-das-clausulas-padrao-da-anpd-se-encerra-em-23-de-agosto/)
- Transferência internacional está no radar fiscalizatório da ANPD. Quem optou pelas CPCs e não as incorporou no prazo pode ser fiscalizado; quem usa outros mecanismos do art. 33 pode seguir em conformidade — [Migalhas Quentes 449475](https://www.migalhas.com.br/quentes/449475/envio-de-dados-ao-exterior-esta-no-radar-fiscalizatorio-da-anpd)
- A Res. CD/ANPD 32, de 26/01/2026, reconhece a União Europeia como "organismo internacional que proporciona grau de proteção de dados pessoais adequado". O art. 5º preserva os demais mecanismos. A Comissão Europeia adotou decisão recíproca sobre o Brasil, em decisões unilaterais e coordenadas — [Legismap – Res. 32/2026](https://legismap.com.br/leis-e-normas/resolucao-anpd-n-032-de-26-01-2026); [Cescon Barrieu](https://cesconbarrieu.com.br/decisao-de-adequacao-reciproca-entre-brasil-e-uniao-europeia-implicacoes-para-fluxos-transfronteiricos-de-dados/); [Lefosse](https://lefosse.com/noticias/alerta/transferencia-internacional-de-dados-pessoais-anpd-anuncia-decisao-de-adequacao-mutua-entre-brasil-e-uniao-europeia/); [Pinheiro Guimarães 29/01/2026](https://pinheiroguimaraes.com.br/publicacoes/decisao-de-adequacao-mutua-entre-brasil-e-europa-beneficia-empresas-e-individuos-ao-reconhecer-a-equivalencia-entre-lgpd-e-gdpr/)
- As fontes divergem sobre o alcance: uma fala em "22 estados-membros", e as demais em 27 Estados-membros (há menção também ao EEE). A versão de 27 é a mais consistente, mas o texto oficial deve ser conferido — resumo de busca baseado em [Confidata](https://confidata.com.br/blog/lgpd-gdpr-transferencia-dados-brasil-europa) e [BMA](https://www.bmalaw.com.br/conteudo/direito-digital-protecao-de-dados-e-cybersecurity/informativos-e-newsletters/reconhecimento-da-decisao-de-adequacao-brasiluniao-europeia/pdf)
- [texto legal] Art. 39: o operador realiza o tratamento segundo as instruções do controlador, que verifica a observância. Art. 42 §1º, I: o operador responde solidariamente quando descumpre a lei ou as instruções lícitas. Art. 46: medidas de segurança. Art. 33: mecanismos de transferência (adequação, cláusulas-padrão, cláusulas específicas, normas corporativas globais, selos etc.) — [LGPD](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709compilado.htm)

### Inferences
- [conhecimento prévio – verificar] Estrutura da Res. 19/2024: o Anexo I é o Regulamento e o Anexo II são as CPCs. As CPCs têm Seção I (definições, partes, objeto, opções A/B/C conforme o papel controlador/operador do exportador e do importador), Seção II (cláusulas obrigatórias, que não podem ser alteradas, sobre responsabilidades, transparência, direitos, segurança, incidentes, transferências posteriores, término e foro brasileiro) e Seção III (medidas de segurança e informações complementares, preenchíveis). As CPCs podem ser incorporadas em contrato próprio ou instrumento autônomo, e há versão em inglês. O art. 17 trata da publicação, em página do site, de documento sobre a transferência (forma, duração, finalidade), com resposta ao titular em 15 dias.
- Contrato de operador (DPA doméstico) para a skill:
  - Objeto, natureza, finalidade e duração.
  - Categorias de dados e de titulares.
  - Tratamento só sob instruções documentadas.
  - Confidencialidade.
  - Medidas de segurança (art. 46; Guia de segurança para agentes de pequeno porte).
  - Suboperadores com autorização e repasse de obrigações.
  - Apoio no atendimento de direitos (prazos dos arts. 18/19).
  - Aviso de incidentes ao controlador em prazo compatível com os 3 dias úteis da Res. 15/2024 (ex.: 24 a 48 h).
  - Apoio a RIPD e ROPA.
  - Devolução ou eliminação ao término.
  - Auditoria.
  - Transferências internacionais (CPCs ou adequação UE).
  - Responsabilidade e indenização.
  - Encarregados e contatos.

### Gaps
- Texto literal das CPCs (Anexo II) e do art. 17 da Res. 19/2024 não acessado. A versão consolidada pós-retificação de 18/08/2025 deve ser obtida no site da ANPD.
- Não foi verificado se existe guia ANPD atualizado sobre agentes de tratamento (controlador/operador) após a versão 2.0 de 2022. [conhecimento prévio – verificar] "Guia Orientativo para Definições dos Agentes de Tratamento de Dados Pessoais e do Encarregado", v1 de maio/2021 e v2 de abril/2022; a parte sobre o encarregado foi em grande medida superada pela Res. 18/2024.
