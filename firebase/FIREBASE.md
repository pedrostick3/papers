# Papers com conta Google (Firebase), opcional

> Neste repositório, o `firebase-config.js` está na raiz e o `firebase.json` está nesta pasta (publica a raiz do repositório). Corre os comandos `firebase` a partir da pasta `firebase/`. Onde este guia diz `public/firebase-config.js`, usa o `firebase-config.js` da raiz.

Este pacote publica o jogo num endereço teu (`https://<id-do-projeto>.web.app`) com entrada por conta Google. O progresso do jogador (jogos terminados, skins compradas e visual escolhido) fica guardado na conta e sincroniza entre telemóveis.

Custo: o plano gratuito do Firebase (Spark) chega para este uso; vê a secção **Custos** no fim.

## 1. Criar o projeto

1. Vai a https://console.firebase.google.com e cria um projeto (o Google Analytics é opcional).
2. **Authentication** > Começar > separador **Sign-in method** > **Google** > Ativar. Escolhe o email de suporte e guarda.
3. **Firestore Database** > Criar base de dados > **modo de produção** > escolhe uma região europeia (por exemplo `europe-southwest1`, Madrid).
4. **Definições do projeto** (roda dentada) > **As tuas apps** > ícone **Web** (`</>`) > regista a app (não precisas de ativar o Hosting aqui).
5. Copia o objeto `firebaseConfig` que aparece e cola-o em `public/firebase-config.js`, no lugar de `null`.
6. Em `.firebaserc`, troca `COLOCA-AQUI-O-ID-DO-PROJETO` pelo ID do projeto.

## 2. Publicar

Precisas de Node.js instalado.

```bash
npm install -g firebase-tools
firebase login
cd papers-firebase
firebase deploy
```

O comando publica o jogo e as regras de segurança da base de dados. No fim mostra o endereço, do tipo `https://o-teu-projeto.web.app`.

## 3. Testar

1. Abre o endereço no telemóvel e toca em **Entrar com Google** no topo do ecrã inicial.
2. Na loja, obtém uma skin e abre o mesmo endereço noutro dispositivo com a mesma conta: o saldo e as skins aparecem lá.

## Domínio próprio (opcional)

1. **Hosting** > Adicionar domínio personalizado e segue os passos de DNS.
2. **Authentication** > Settings > **Authorized domains** > adiciona o domínio. Sem isto, o login Google é recusado nesse domínio.

## Como funciona a sincronização

- Sem sessão iniciada, tudo fica no telemóvel, como antes.
- Ao entrar pela primeira vez, o progresso que já existia no telemóvel junta-se ao da conta: somam-se os jogos terminados e as skins de ambos os lados, sem duplicar.
- Se entrar outra conta no mesmo telemóvel, ela não herda o progresso da anterior.
- O saldo é calculado a partir dos jogos terminados menos o preço das skins compradas, por isso juntar dois dispositivos nunca duplica jogos.
- Na base de dados fica um documento por jogador em `players/<email>`, com o email em minúsculas como identificador. O documento guarda também o `uid` do Firebase e o nome, o que facilita encontrar e depurar um jogador na consola.
- Como o email fica guardado, deves referi-lo na política de privacidade do jogo (RGPD).
- O jogador pode apagar os seus dados no ecrã **Conta**.

## Limitações

- O jogo corre todo no telemóvel, por isso alguém com conhecimentos técnicos consegue alterar o seu próprio saldo. Como as skins são só cosméticas, o risco é baixo. Para o impedir, a atribuição de jogos teria de passar para uma Cloud Function.
- A biometria do admin passa a funcionar normalmente, porque o jogo deixa de estar dentro de uma página embutida.

## Custos (plano gratuito Spark)

Limites gratuitos relevantes para o Papers (confirma sempre em https://firebase.google.com/pricing):

| Serviço | Limite gratuito | Uso do Papers |
| --- | --- | --- |
| Authentication (Google) | 50 000 utilizadores ativos por mês | 1 por jogador |
| Firestore: leituras | 50 000 por dia | cerca de 2 por login |
| Firestore: escritas | 20 000 por dia | 1 por login, compra ou jogo terminado |
| Firestore: armazenamento | 1 GiB | cerca de 1 KB por jogador |
| Hosting: transferência | 360 MB por dia | cerca de 40 KB por visita (comprimido) |

O primeiro limite a chegar é a transferência do Hosting, por volta de milhares de visitas por dia. As bibliotecas (three.js, anime.js e o SDK do Firebase) vêm de CDNs externas e não contam.

Se um limite for ultrapassado no plano gratuito, o serviço para até ao período seguinte; não há cobranças. No plano Blaze (pago por uso) não existe teto de gastos para o Firestore e o Hosting, só alertas de orçamento.
