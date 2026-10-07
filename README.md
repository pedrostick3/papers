# Papers

Jogo de festa dos papelinhos, jogado num só telemóvel: o telemóvel do dono é o balde.

**Jogar:** https://pedrostick3.github.io/Papers/

## Como se joga

1. Formem 2 ou mais equipas, com pelo menos 2 pessoas cada.
2. Cada pessoa escreve 3 palavras em segredo. Vão todas para o balde.
3. Em cada turno de 60 segundos, um jogador tira papelinhos ao calhas e dá pistas à sua equipa. Não se passam palavras.
4. Ronda 1: descreve. Ronda 2: mímica. Ronda 3: uma só palavra. As palavras são sempre as mesmas.
5. Ganha a equipa que adivinhar mais papelinhos nas 3 rondas.

## O que tem

- Balde 3D numa mesa, com os papelinhos lá dentro e animações (three.js e anime.js).
- Jogador da vez sorteado dentro da equipa, sem ninguém repetir antes de todos jogarem.
- Botão de pausa com alarme alto, para toda a mesa ouvir.
- Definições por partida: duração do turno, papelinho em espera, falta, tempo que sobra, som e vibração.
- Dois modos: um só telemóvel, passado de mão em mão, ou uma sala com um telemóvel por equipa.
- Menu admin (roda dentada) protegido por PIN ou biometria: desfazer jogadas, ajustar pontos, mudar regras a meio.
- Loja e provador de skins (balde, mesa, papelinhos e fitas), pagas com jogos terminados.
- Guarda o jogo a meio: se o browser fechar, o botão "Continuar jogo" retoma a partida.

## Modo sala (um telemóvel por equipa)

1. Na preparação, em **Telemóveis**, escolhe **Um por equipa** e toca em **Criar sala**.
2. O telemóvel do dono mostra um código de 5 letras e um QR code. Cada equipa lê o QR com a câmara, ou abre o jogo, toca em **Entrar numa sala** e escreve o código.
3. Cada equipa escolhe a sua equipa e os seus jogadores escrevem as palavras no telemóvel da equipa. As palavras caem no balde do dono.
4. Nos turnos, o jogador da vez joga no telemóvel da equipa. O telemóvel do dono fica na mesa com o balde 3D e o tempo, sem mostrar a palavra.

Se um telemóvel perder a ligação, o turno fica em pausa e o dono pode continuá-lo no seu telemóvel. Uma equipa sem telemóvel pode escrever e jogar no telemóvel do dono.

Para os telemóveis se encontrarem, o jogo usa o servidor público e gratuito do PeerJS (sem conta nem configuração). Depois de ligados, os telemóveis comunicam diretamente; se a rede não o permitir, a ligação passa pelos servidores de reencaminhamento do PeerJS.

Para testar no computador sem rede, abre vários separadores com `?rede=local` no fim do endereço.

## Publicar no GitHub Pages

1. Envia os ficheiros deste repositório para o ramo `main` (pelo site: **Add file > Upload files**).
2. Em **Settings > Pages**, escolhe **Deploy from a branch**, ramo `main`, pasta `/ (root)`, e guarda.
3. Ao fim de um ou dois minutos o jogo fica em https://pedrostick3.github.io/Papers/.

O repositório tem de ser público para usar o GitHub Pages com uma conta gratuita.

## Progresso

O jogo em curso, as skins e os jogos ganhos ficam guardados no browser do telemóvel do dono. Não há contas nem servidor.

A pasta `firebase/` tem uma integração opcional com contas Google, desligada por omissão (`firebase-config.js` está a `null`). Só é preciso se quiseres guardar o progresso na nuvem; vê `firebase/FIREBASE.md`.

## Tecnologia

Um único ficheiro `index.html` com HTML, CSS e JavaScript, sem build. Bibliotecas carregadas por CDN: three.js r128, anime.js 3.2.2, PeerJS 1.5.5 e qrcode-generator 2.0.4 (estas duas só no modo sala).
