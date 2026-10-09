# Controley — Android

Aplicativo independente para controlar uma TV LG com webOS pela rede local. Interface em português, sem conta, anúncios ou servidor próprio. Versão 1.10.0 (versionCode 44), nome **Controley**, pacote `br.com.controledasala.integrado` (o mesmo da 0.4.1 “Controle da Sala +”).

## Instalar e conectar

1. Transfira o APK para o celular e abra o arquivo. Se o Android pedir, permita a instalação para o aplicativo usado para abrir o APK.
2. Ligue a TV. Conecte o celular e a TV à mesma rede Wi-Fi, sem isolamento de dispositivos ou rede de convidados.
3. Abra o **Controley**. Na primeira vez ele procura as TVs da rede sozinho; toque na sua TV na lista. **Conectar pelo IP** fica por último, para quando a busca não encontrar a TV.
4. Aceite a solicitação na tela da TV usando o controle físico. A chave de pareamento e o certificado ficam salvos no armazenamento privado do aplicativo.
5. Nas próximas aberturas, o aplicativo reconecta sozinho à última TV.

Android mínimo: 8.0 (API 26). A 0.5.0 é assinada com a mesma chave da 0.4.1 e tem versionCode maior, então instala por cima sem desinstalar e deve manter o pareamento. Ela não instala por cima da 0.4.0 (pacote e chave diferentes); para quem vem da 0.4.0 é instalação nova, com novo pareamento. Publicação na Play Store não está incluída nesta entrega.

## Novidades da 1.11.0 — relato com foto e perguntas frequentes

- **Relato mais completo.** O formulário pergunta a marca (já preenchida com a da TV conectada) e o modelo da TV, e aceita até duas fotos da TV ou da etiqueta atrás dela. As fotos são reduzidas (até 1600 pixels, abaixo de 600 KB) e regravadas, o que apaga data, local e outros dados escondidos. Elas vão para um armazenamento privado e ficam 60 dias. Quem lê é só o mantenedor, por uma chave secreta.
- **Botão "Relatar" nas telas de ajuda.** Os cartões de orientação, o código/PIN, o IP, a busca de TVs, "Como conectar", os comandos de voz e "TVs compatíveis" levam direto ao relato (e ao FAQ).
- **Perguntas frequentes** em Ajustes e na tela inicial: 19 perguntas em português, inglês e espanhol, com busca sem acento. A lista vem de `faq.json` no repositório de releases e se atualiza sozinha, sem versão nova.
- **Servidor:** função `controley_submit_report_v2` (marca e modelo), colunas `tv_brand`, `tv_model`, `photos` e `analysis`, e a função de borda `controley-photo` (recebe e valida fotos JPEG; leitura só com o token do mantenedor).
- Não verificado em celular: o formulário, a escolha de fotos e a tela de FAQ passaram só por testes automáticos e por um envio completo ao servidor feito por script.

## Novidades da 1.10.0 — cores de destaque

- Ajustes > Aparência > **Cor de destaque**: verde (padrão), azul, vermelho, rosa, roxo e **Do sistema** (acompanha o papel de parede, Android 12 ou superior). Vale para os temas claro e escuro, para o botão flutuante e para todo o app.
- As cores nasceram de um estudo de preferência e acessibilidade (`ESTUDO-DE-CORES.md`): azul lidera as pesquisas de cor favorita; o roxo foi incluído por ser a segunda ou terceira em vários países.
- Os estados da conexão (conectada em verde, aguardando em âmbar, desligada em vermelho) não mudam com o destaque.
- Todas as paletas passam nos alvos de contraste (testes automáticos para os dois temas e para qualquer cor de papel de parede).
- Não testado em celular nem TV; as cores foram conferidas por cálculo e por testes automáticos (249), não pela tela de um aparelho.

## Novidades da 1.9.0 — central de notificações

- Ajustes > **Notificações**: caixa de entrada com os comunicados, e **Preferências** com chaves por categoria (atualizações do app, novidades, dicas, respostas aos relatos). Avisos importantes não podem ser desligados. O app orienta quando a permissão de notificação do Android está desligada.
- Comunicados publicados pelo desenvolvedor, com idioma (pt, en, es), segmentação por versão, marca da TV e idioma, liberação gradual, agendamento, validade, botão de ação e métricas (entregue, aberto, tocou, dispensou). Um cartão na aba Controle mostra o mais importante ainda não lido.
- **Aviso de versão nova** automático, mesmo com o app fechado, sem precisar publicar comunicado.
- Todas as notificações passam por um único componente (canais por categoria, permissão, sem repetir, silêncio das 22h às 7h, exceto avisos importantes). O botão flutuante e o envio de mídia continuam com a notificação própria que o Android exige enquanto rodam.
- Tocar na notificação abre a tela certa (caixa de entrada, relatos ou a atualização).
- Guia para publicar comunicados e consultar métricas: `NOTIFICACOES.md`.
- Não testado em celular nem TV; a rede foi testada contra o banco real e a lógica por testes automáticos (243).

## Novidades da 1.8.1

- A verificação de respostas aos relatos com o app fechado passou de ~3 h para ~20 min (enquanto houver relato aberto). Texto "1 enviado" no singular.

## Novidades da 1.8.0 — relatos de problemas

- Ajustes > **Relatar um problema**: o usuário escolhe o assunto, descreve o que aconteceu e envia. Antes de enviar, **Ver o que será enviado** mostra o diagnóstico: versão do app, modelo do celular e do Android, marca da TV, estado da conexão e os últimos eventos, com endereços IP, MAC e e-mails ocultados. Nome, contatos e arquivos nunca vão.
- A resposta volta ao app (cartão na aba Controle e **Meus relatos**) e por notificação, mesmo com o app fechado (verificação a cada ~20 min enquanto houver relato aberto; o Android pode adiar um pouco para poupar bateria). Nas correções, os botões **Funcionou** e **Ainda falha** fecham ou reabrem o relato.
- Na falha de conexão repetida, a tela da TV mostra o botão **Relatar problema**.
- O texto digitado fica guardado se o envio falhar. Limite de 5 relatos por dia por aparelho.
- Backend: banco Supabase só do Controley. A chave pública embutida só chama três funções (enviar, listar os relatos do próprio aparelho, responder); não lê nem escreve a tabela diretamente. O aparelho se identifica por um código aleatório gerado no próprio app.
- Não testado em celular nem TV; a parte de rede foi testada contra o banco real e a lógica por testes automáticos (234).

## Novidades da 1.0.1 — revisão e polimento

- Barra inferior: os nomes das abas agora ficam centralizados sob os ícones (antes ficavam encostados à esquerda).
- Teclas coloridas: "Vermelho" não quebra mais em duas linhas; o texto encolhe para caber.
- Teclas desativadas ficam mais legíveis. "Desligar em…" também fica desativado sem TV conectada (cancelar continua disponível).
- Mais: a análise de Limpeza abre logo abaixo de "Limpeza de apps", e Botão flutuante e Ajustes ficam em outro cartão.
- Sem TV: o aviso "Nenhuma TV conectada ainda." não se repete sob o título "Conecte sua TV", e a aba Digitar mostra só o campo de texto e os botões de busca, sem a ilustração grande.
- Não testado em celular nem TV.

## Novidades da 1.0.0 — redesenho

Interface nova, desenhada a partir do design system **Controley** (tokens, componentes e telas). Nenhuma mudança em conexão, protocolo, descoberta, ligar pela rede, mídia ou atualização.

- **Navegação:** barra inferior com Controle, Digitar (antes "Teclado"), Apps e Mais. Deslizar entre telas continua funcionando.
- **Topo de toda tela:** chip de status da conexão (verde conectada, âmbar esperando, vermelho TV desligada, cinza sem TV; toque para detalhes), microfone (segure para ver os comandos) e Desligar TV com confirmação (com a TV desligada, o mesmo botão liga pela rede).
- **Controle:** direcional circular com OK verde (segurar uma seta repete), Voltar · Início · Entradas, volume em balancim com o nível da TV (− e + repetem ao segurar; arraste a barra para escolher) e Mudo. Favoritos no topo, segurar tira dos favoritos.
- **Digitar:** faixa de estado do campo da TV, campo grande, Ao vivo / Ao tocar, Ditar · Apagar · Enter/Enviar e um direcional pequeno para navegar nos resultados sem trocar de tela.
- **Apps:** grade de ícones com Favoritos (até 8) separados de Todos.
- **Mais:** Reprodução, Canais, Menu da TV, Teclas coloridas (com o nome escrito), Limpeza de apps, Botão flutuante e Ajustes do app.
- **Ajustes:** tela própria em grupos (TV, Controle, App, Conexão) com interruptores, no lugar do diálogo de 15 itens.
- **Escolhas e confirmações** em folhas que sobem do rodapé (Desligar em, Entradas, Teclado numérico, Aparência, Idioma, TVs salvas, Conexão). IP, MAC e busca de TVs continuam como diálogos, no tema do app.
- **Temas:** Automático (segue o Android), Escuro e Claro, com o verde-lima do ícone. Quem usava um dos 6 temas antigos cai no Escuro ou Claro equivalente.
- **Ícones:** conjunto novo de 56 ícones (traço 2, grade 24) em `RemoteIcon`, também no widget, nos blocos rápidos e no botão flutuante.
- Novo: `Kit.java` (tokens de cor e componentes). Fonte: a do sistema (o empacotador não tem recursos de fonte; a Figtree do design system ficou de fora).
- ~120 textos novos ou que não tinham tradução ganharam inglês e espanhol em `L.java`.
- Não testado em celular nem TV.

## Novidades da 0.9.1

- Botão flutuante mais robusto: a janela agora ocupa a tela inteira (inclusive apps em tela cheia e com entalhe) e o serviço volta sozinho se o Android o encerrar enquanto o botão está ligado.
- O Android permite que cada app esconda janelas sobrepostas (bancos e alguns apps de pagamento fazem isso) e alguns fabricantes têm opções extras para janelas em segundo plano. O Controley não consegue contornar isso.
- Não testado em celular nem TV.

## Novidades da 0.9.0

- Botão flutuante: um botão redondo que fica por cima de qualquer app (Facebook, YouTube, galeria…). Toque nele para abrir um controle com Voltar, Início, setas, OK, volume, mudo, reproduzir, pausar e desligar; toque fora, ou no botão de minimizar, para fechar. Arraste o botão para onde preferir.
- Setas e volume repetem quando você segura. Desligar pede um segundo toque em até 3 segundos.
- Ative em Configurações > "Ativar botão flutuante" ou pelo bloco "TV: Botão flutuante" das configurações rápidas. O Android pede a permissão "Aparecer sobre outros apps", que só você pode conceder.
- O painel conecta à TV quando abre (usando o pareamento já salvo) e solta a conexão 30 segundos depois de fechar. Uma notificação com o botão Desativar fica visível enquanto o botão flutua.
- Novos: FloatService e FloatTile. Não testado em celular nem TV.

## Novidades da 0.8.2

- Fotos agora são enviadas ao player de mídia da própria TV (UPnP/DLNA: o Controley procura o "media renderer" da TV, manda o endereço da foto e o comando de reproduzir). Não precisa de pareamento para isso, só da TV ligada no mesmo Wi-Fi.
- Se a TV não oferecer esse player ou recusar a foto, o Controley cai no navegador da TV, como na 0.8.1, que funcionou.
- Vídeos continuam pelo visualizador de mídia do webOS, como na 0.8.0, que funcionou.
- Não testado em celular nem TV. 92 testes.

## Novidades da 0.8.1

- Correção do envio de fotos: a TV não mostrava a foto pelo visualizador de mídia, então agora as fotos abrem no navegador da TV, em uma página preta com a imagem ajustada à tela. Vídeos continuam como na 0.8.0, que funcionou.
- Fotos em formatos que a TV não abre (como HEIC) são convertidas para JPEG no celular antes do envio.
- Não testado em celular nem TV.

## Novidades da 0.8.0

- Enviar foto ou vídeo para a TV: na galeria, toque em Compartilhar e escolha "Enviar para a TV (Controley)". O celular serve o arquivo pela rede Wi-Fi (servidor HTTP próprio, com suporte a avançar no vídeo) e o Controley manda a TV abri-lo.
- Funciona com a TV já pareada e no mesmo Wi-Fi. Uma foto ou um vídeo por vez.
- Enquanto o arquivo é servido aparece uma notificação com o botão Parar; o envio também termina sozinho depois de 4 horas.
- Sem internet nem nuvem: o arquivo vai direto do celular para a TV, por um endereço aleatório que só existe durante o envio.
- A TV é aberta pelo visualizador de mídia do webOS; se ele recusar, o Controley tenta o navegador da TV. Não testado em celular nem TV.
- Novos: MediaServer, ShareService e ShareActivity, com 8 testes de servidor (84 no total).

## Novidades da 0.7.2

- Widget na tela inicial com Vol −, Mudo, Vol + e Desligar. Cada toque usa uma conexão curta com a TV já pareada.
- O empacotador (tools/package-apk.mjs) agora gera o layout do widget, o arquivo do provedor e os ids das views direto na tabela de recursos, sem AAPT2.
- Não testado em celular nem TV.

## Novidades da 0.7.1

- Os botões de volume do celular mudam o volume da TV enquanto ela está conectada e o app está aberto. Dá para desligar isso em Configurações.
- Quatro blocos para as configurações rápidas do Android: TV: Mudo, TV: Vol +, TV: Vol − e TV: Desligar. Cada toque abre uma conexão curta com a TV já pareada, faz a ação e fecha.
- Não testado em celular nem TV.

## Novidades da 0.7.0

- Quando o Wi-Fi ou a rede cabeada do celular volta, o app tenta reconectar à TV na hora.
- Depois das quatro tentativas rápidas, uma TV já pareada é tentada de novo a cada 30 segundos enquanto o app está aberto. O aviso de falha aparece uma vez só.
- Configurações → TVs salvas lista as TVs pareadas neste celular e troca entre elas com um toque.
- Não testado em celular nem TV.

## Novidades da 0.6.15

O teclado passa a usar o aviso da TV. A tela diz se há um campo aberto. Sem esse aviso, Enviar, o modo ao vivo, apagar e ditar não mandam texto. YouTube e Netflix usam o teclado do próprio app e continuam sem receber o texto do celular. Nesses, a busca por voz segue o caminho.

## Novidades da 0.6.14

No touchpad, a faixa da direita rola com um dedo. Arrastar para cima ou para baixo nela faz o mesmo que os dois dedos. Um toque nessa faixa não clica.

## Novidades da 0.6.13

Em Configurações, Aparência deixa escolher a paleta. São seis: Azul escuro (a padrão), Verde escuro, Âmbar escuro, Azul claro, Verde claro e Claro.

## Novidades da 0.6.12

O Controle deixa de ser uma ficha de seções. Some os títulos Seus apps, Navegação, Volume e Acesso rápido. As setas ficam maiores. Setas e Touchpad viram um seletor baixo, não mais dois botões do tamanho do controle. O volume é uma linha só: menos, nível, mais e mudo. Exemplos sai da tela; segurar Falar comando continua abrindo a lista. Os botões encolhem de leve ao toque.

## Novidades da 0.6.11

Nova paleta. O fundo deixa de ser verde-escuro e passa a um grafite neutro, com cartões em azul-ardósia. O azul claro é a única cor de ação: botão principal, aba ligada, volume e status de conectado. Desligar continua rosa. Os quatro botões de cor da TV seguem vermelho, verde, amarelo e azul, para bater com o controle físico.

## Novidades da 0.6.10

No Controle, Setas e Touchpad ficam da mesma altura, com o ícone ao lado do nome. Os apps em Seus apps usam duas linhas, para o nome não cortar no meio. O aviso “Conecte a TV primeiro” some quando a TV já está conectada, e a leitura automática do volume não dispara esse aviso.

## Novidades da 0.6.9

A aba Apps mostra os aplicativos da tela inicial da TV. A lista completa da TV inclui páginas de ajuste, entradas HDMI e serviços internos, e esses ficam de fora. A Limpeza continua lendo a lista completa.

## Novidades da 0.6.8

As mesmas cores, com um papel cada. O verde preenchido é a ação principal da tela (Clique ou OK, Enviar, Ligar a TV). A borda verde marca o que está ligado: aba, modo do teclado e mudo. Favorito virou um ponto verde, não uma borda. O texto verde do topo só aparece com a TV pronta; enquanto conecta, o ponto ao lado fica âmbar. Desligar pinta o botão inteiro de rosa. Aviso âmbar só quando algo pede atenção. A barra de volume usa o verde do app.

## Novidades da 0.6.7

Em Configurações, Idioma oferece português do Brasil, inglês e espanhol. Sem escolha salva, o app segue o idioma do celular quando ele é inglês ou espanhol, e português nos demais. A voz usa o mesmo idioma.

## Novidades da 0.6.6

O Controle abre nos seus apps, com nome e ícone, e não mostra mais o identificador técnico. O touchpad ficou mais baixo e o Clique não ocupa a linha inteira. Legenda e Áudio foram para Mais. Com a TV ligada, Mais mostra só Desligar. A limpeza passou a se chamar Limpeza.

## Novidades da 0.6.5

O volume mostra o nível e aceita um controle deslizante. No Controle, Seus apps reúne os favoritos e os que você abriu por último. Segure um app na aba Apps para favoritar. Legenda e Áudio mandam as teclas CC e SAP da TV. Em Mais, Desligar em… marca 15, 30, 60 ou 90 minutos e a TV desliga mesmo com o app fechado.

## Novidades da 0.6.4

No touchpad, Voltar e Início ficam só no acesso rápido. No Teclado, o modo selecionado não usa mais o mesmo verde do botão de enviar, e Limpar trocou o ícone de mais por um X. Em Apps, o botão passou a se chamar Atualizar a lista e o nome do app não quebra no meio da palavra. Em Mais, as quatro cores viraram teclas coloridas numa linha só.

## Novidades da 0.6.3

A Limpeza saiu da barra de abas e foi para o fim de Mais. A última análise fica salva no celular e a lista continua ordenada pelo tamanho. O botão Lista na TV abre a tela inicial, onde a exclusão é feita.

No Teclado, o campo de texto vem primeiro. Ditar, Enviar ou Enter e Apagar ficam na mesma linha. O modo ao vivo continua, mas abaixo do campo.

## Novidades da 0.6.2

Corrige as setas da aba Controle, que na 0.6.1 esticavam a primeira linha e escondiam as outras. As cinco teclas voltam a aparecer e a responder.

## Novidades da 0.6.1

Ajustes de tela medidos na revisão da 0.6.0, sem mudança de função.

- O aviso de atualização saiu do topo da aba Controle e foi para o final, depois do volume. **Atualizar** e **Agora não** continuam iguais.
- A barra de busca da TV entrou na área que rola. Em tela deitada ela não cobre mais o controle.
- A aba Controle começa por navegação e volume. O comando de voz ficou num botão só; os exemplos abrem ao segurar ou em **Exemplos**. O texto de exemplo deixou de ocupar a tela o tempo todo.
- As explicações longas do teclado, da Limpeza e das notas de atualização quebram em mais de uma linha.

## Novidades da 0.6.0

### Aba Limpeza

**Analisar a TV** lê a lista de apps instalados (a mesma permissão da aba Apps, nada é alterado na TV) e mostra:

- **Resumo:** quantos apps podem ser removidos e quanto ocupam, quantos têm nome repetido, quantos estão sem uso recente e quantos são do sistema (ficam de fora).
- **Nome repetido:** dois apps com o mesmo nome, em geral uma versão antiga esquecida.
- **Sem uso recente:** removíveis instalados há mais de 90 dias que o Controley não abriu nesse período. Só conta o que foi aberto pelo Controley (abas Apps, Limpeza e voz), porque a TV não informa o uso dos apps.
- **Podem ser removidos:** todos os apps que a TV marca como removíveis, do maior para o menor, com versão, tamanho e data de instalação.

A TV não permite desinstalar por um app externo. Cada item tem **Abrir na TV**, e o aviso explica como confirmar a remoção na tela da TV (segurar OK sobre o app e tocar no X, ou Editar lista de apps nas TVs mais novas).

A TV também não informa se um app está desatualizado ou foi descontinuado na loja da LG, então a auditoria não promete isso; as atualizações de apps continuam pela própria TV.

Validação: 71 testes unitários passaram (4 novos da auditoria). Não testado numa TV real.

## Novidades da 0.5.0

### Nome

O app passa a se chamar **Controley** (ícone, título, pedido de pareamento na TV e agente HTTP). O pacote não mudou, para a atualização entrar por cima da 0.4.1.

### Formas de conectar, da mais fácil para a mais técnica

1. **Automática:** ao abrir, reconecta à última TV usada.
2. **TV mudou de IP:** se a última TV não responde, o app procura na rede uma TV com o mesmo MAC ou o mesmo nome. Achando, move o pareamento salvo para o novo endereço e reconecta sem pedir nada. Isso roda uma vez por endereço em cada sessão, e o certificado salvo da TV continua sendo conferido.
3. **Um toque na lista:** sem conexão, a tela de controle mostra as TVs encontradas na rede (até 4), com a última usada marcada. Tocar conecta.
4. **Reconectar:** tenta de novo a última TV.
5. **Ligar TV:** acorda a TV pela rede (Wake-on-LAN), quando o MAC já é conhecido.
6. **Buscar TVs:** nova busca na rede (SSDP, mDNS e varredura das portas do webOS).
7. **Conectar pelo IP:** último recurso, digitando o endereço visto nas configurações de rede da TV.

As mesmas opções ficam em ⋮ → Configurações, junto com **Ajuda**, que explica essa ordem. Na primeira abertura, sem TV salva, a busca começa sozinha.

### Atualização automática

Mesmo esquema do Treney. O app lê `update.json` do repositório público [controley-releases](https://github.com/diegocruzd3/controley-releases) ao abrir e ao voltar para o app, no máximo a cada 30 minutos (ou na hora, em Configurações → **Procurar atualização**).

Quando há versão com `versionCode` maior, aparece um aviso na aba Controle com **Atualizar** e **Agora não**. **Agora não** esconde só aquela versão. O download aceita apenas APK das Releases desse repositório, por HTTPS e redirecionamentos do GitHub, até 50 MB. Antes de abrir o instalador do Android, o app confere se o arquivo é o mesmo pacote com o `versionCode` anunciado. Se o Android ainda não permitir “Instalar apps desconhecidos” para o Controley, o app abre essa tela e continua a instalação quando você volta.

Quem está na 0.4.1 precisa instalar a 0.5.0 manualmente uma vez, porque a 0.4.1 não tem o atualizador. Daí em diante as versões chegam pelo app.

**Publicar uma versão nova:** aumente `versionCode` e `versionName` (em `tools/package-apk.mjs` e `app/build.gradle`), gere o APK com a **mesma keystore** e crie a Release `vX.Y.Z` com o asset `controley.apk`. Por último, atualize `update.json` na branch `main`. Com outra chave o Android recusa a atualização.

### Validação da 0.5.0

67 testes unitários passaram, incluindo os novos de leitura do `update.json`, links confiáveis, regra de 30 minutos, “Agora não” e reencontro da TV por MAC ou nome. O APK foi verificado com apksigner, zipalign e aapt. O `update.json` publicado e o download do `controley.apk` pelo redirecionamento do GitHub foram conferidos. Nada disso foi testado num celular ou numa TV reais, e o lint do Android não foi rodado (não há Gradle neste pipeline).

## Melhorias da versão 0.2

Na atualização 0.2.2, controles e cards recebem superfícies mais claras e contornos. Botões desabilitados têm cores próprias, com textos preservados. Ícones vetoriais desenhados pelo app identificam reprodução, pausa, navegação, volume, entradas, energia e abas. Mudo mostra a ação **Silenciar** ou **Ativar som**, mantendo descrição do estado para acessibilidade.

É possível deslizar horizontalmente na área de conteúdo para a tela vizinha; as abas continuam disponíveis por toque. A troca se conclui ao soltar após um arrasto suficiente, com transição curta. Gestos curtos cancelam o toque original e não trocam de tela. Movimentos verticais permanecem rolagem, bordas são reservadas ao sistema, campos de texto preservam seleção e o gesto de páginas fica desativado na exploração por toque do TalkBack. A primeira e última tela não formam um ciclo. Rascunho e rolagem são mantidos.

O cabeçalho de conexão permanece estável; toque nele para detalhes, busca ou reconexão. Avisos de comandos aparecem na tela de origem, sem duplicação com Toast e sem sumir por atualização de áudio. O teclado recebe campo delimitado, Enviar destacado e validação de texto vazio. Busca/favoritos de apps, repetição ao segurar e tema claro continuam como etapas futuras.

Na atualização 0.2.1, a aba Apps passa a usar cards com logo e nome. A grade tem uma a cinco colunas conforme a largura disponível e reduz a quantidade com fontes ampliadas. O app consulta `listApps` e enriquece os mesmos IDs com os ícones de `listLaunchPoints`, conforme o [Connect SDK](https://github.com/ConnectSDK/Connect-SDK-Android-Core/blob/master/src/com/connectsdk/service/WebOSTVService.java).

Os logos são carregados fora da interface, com cache de imagens de até 8 MB em memória, downloads limitados, tamanho máximo e redução de resolução. HTTPS da TV usa o certificado já memorizado no pareamento; servidores públicos usam a validação normal do Android. Caminhos internos da TV não são arquivos disponíveis no celular. Quando a TV não fornece uma URL acessível, há uma inicial no lugar do logo. O nome e a ação de abrir o app continuam disponíveis. Depois de atualizar, use **Atualizar aplicativos** para carregar os metadados dos logos. Alguns ícones externos dependem de internet. A aparência e as URLs reais ainda precisam de validação na TV.

- Controle principal com direcionais, OK, Voltar, Início, Entradas, volume e mudo; extras na aba Mais.
- Cabeçalho compacto, abas selecionadas, efeito de toque e vibração opcional.
- Composição em duas áreas para largura útil a partir de 560 dp; altura dos botões flexível para fontes grandes, rolagem em telas com pouca altura e abas em duas linhas em janelas estreitas.
- Rascunho do teclado, lista de apps, aba e rolagem preservados entre abas e rotações. Apps são mantidos em memória por TV, sem reutilizar a lista ao trocar de endereço.
- Sessão independente da Activity, sem desconexão durante rotação; pausa ao sair do app e retomada ao voltar.
- Recuperação automática de conexão pareada em até quatro tentativas com espera de 1, 2, 4 e 8 segundos. Comandos antigos não são repetidos.
- Direcionais habilitados apenas após a conexão do socket de navegação; recuperação desse socket separada da conexão de áudio.
- Mudo consultado na TV e atualizado após confirmação, com toques rápidos processados em sequência.
- Desligamento confirmado pelo usuário, bloqueio de comandos durante o desligamento e encerramento sem tentativa automática de ligar novamente.
- Rótulos acessíveis, estado da aba, descrição do mudo e anúncio do estado de conexão.

## Funções implementadas

- Descoberta SSDP de TVs webOS e conexão manual por IPv4 privado.
- Pareamento por autorização na TV, chave persistida por IP e reconexão automática à última TV.
- Conexão WSS na porta 3001, com certificado memorizado após o primeiro pareamento. Opção explícita de WS na porta 3000 para modelos que necessitem dela.
- Direcionais, OK, voltar, início, menu, sair, ajustes e botões coloridos.
- Volume, mudo, canais e teclado numérico.
- Play, pausa, avanço e retrocesso.
- Envio de texto, Enter e exclusão de caracteres em campos compatíveis.
- Listagem e abertura dos aplicativos instalados na TV.
- Listagem e seleção de entradas externas.
- Desligamento e envio de Wake-on-LAN com MAC informado pelo usuário.
- Vibração opcional e mensagens de conexão/erro.

## Limites de validação

O modelo LG webOS UQ7500PSF é a referência inicial informada pelo usuário, ainda sem confirmação do modelo da sua TV. O usuário instalou a versão 0.1.0 e confirmou pareamento, navegação, seleção, volume e mudo em uma TV física. A versão 0.2.2 foi compilada e verificada por ferramentas, com 30 testes JUnit de protocolo, estado da interface e sessão simulada. Ainda precisa de teste no celular e na TV, incluindo TalkBack, rotação e fontes de 100%, 150% e 200%. Firmware, rede e aplicativos podem mudar quais comandos estão disponíveis. Wake-on-LAN depende de suporte e configuração da TV; enviar o pacote não confirma que ela ligou.

Não há modo de demonstração nem TV simulada na interface. Os botões remotos ficam desabilitados até o pareamento real. Se o IP mudar, informe o novo endereço. Para substituir a TV no mesmo IP, use **Refazer pareamento** após confirmar o endereço.

## Compilar

Abra esta pasta no Android Studio e instale o SDK Android 35. Use JDK 17 e o Gradle Wrapper 8.9.

```powershell
.\gradlew.bat assembleDebug testDebugUnitTest lintDebug
```

APK de saída: `app/build/outputs/apk/debug/app-debug.apk`.

O caminho local do SDK em `local.properties` é específico de cada máquina e não faz parte do arquivo ZIP de código-fonte. A variável opcional `CONTROLE_DEBUG_KEYSTORE` permite reutilizar uma chave local de testes; sem ela, o Android Gradle Plugin usa sua chave padrão.

### Empacotamento alternativo no Windows

A ferramenta nativa AAPT2 encerrou com erro de acesso à memória neste ambiente, inclusive para um manifesto mínimo. O APK entregue foi montado pela alternativa incluída em `tools`, usando o compilador Java do JDK, o D8 do Android SDK, manifesto e recursos binários no formato Android e assinatura pelo `apksigner` oficial. O manifesto, a atividade inicial, os recursos, a assinatura e o alinhamento foram conferidos com ferramentas do SDK.

Com Node.js, JDK 17 e SDK Android 35/Build Tools 35 instalados, execute:

```powershell
.\tools\build-portable.ps1 -SdkRoot 'C:\Android\sdk' -JdkRoot 'C:\Java\jdk-17'
```

Saída: `build-portable/Controley-0.6.1.apk`. A primeira execução baixa as dependências Java e cria uma chave de desenvolvimento caso não seja informado `-KeyStore`. Para atualizar o APK entregue, use a chave original já preservada neste ambiente; ela não é distribuída no ZIP. O empacotador alternativo define o manifesto e os recursos explicitamente; ao alterar permissões, versão, nome, pacote ou tema, atualize também `tools/package-apk.mjs`.

## Referências de protocolo

Implementação própria de mensagens SSAP e de descoberta SSDP, consultando o código público do [Connect SDK](https://github.com/ConnectSDK/Connect-SDK-Android-Core) e a [documentação Android](https://developer.android.com/build). Não foram utilizados código-fonte, imagens ou identidade do aplicativo de referência. Sem vínculo com LG ou ControllaTV.

Dependência de rede: OkHttp 3.14.9 (Apache 2.0), com Okio transitivo. As dependências e suas versões estão no arquivo `app/build.gradle`.

## Novidades da 0.4.1 (layout 0.2.2 + recursos da 0.4.0)

- **Controle:** botão “Falar comando” (voz em português pelo reconhecedor do Android; segure ou toque em “Exemplos” para ver os comandos) e seletor “Setas | Touchpad” em Navegação. O touchpad move o cursor, clica com toque curto, rola com dois dedos e tem os botões Clique, Voltar e Início; ele nunca troca de aba.
- **Teclado:** modos “Ao vivo” (envia só o que mudou, com espera curta e confirmação da TV) e “Enviar ao tocar”, além do botão “Ditar texto”.
- **Mais › Ligar TV:** Wake-on-LAN com o MAC salvo para cada TV (aprendido ao conectar ou digitado no menu ⋮ › “MAC para ligar a TV”) e novas tentativas de conexão depois do sinal.
- **Buscar TVs:** SSDP com vários alvos, o último IP, uma varredura limitada das portas 3000/3001 e uso da rede Wi-Fi/Ethernet local mesmo com VPN.
- Build no Linux: `tools/build-box.sh <jdk> <sdk> <deps> <keystore> [saida]`.
