# Ghost Multiplayer

Variação multiplayer do jogo **Ghost** implementada em **Jack** para a plataforma **Hack/nand2tetris**. O projeto foi desenvolvido no contexto da disciplina **Elementos de Sistemas Computacionais** da UFRPE, seguindo a metodologia *Nand to Tetris*, a partir da especificação do Projeto 6.

## Visão geral

Dois jogadores competem ao mesmo tempo:

- **Jogador 1 (Ghost):** controla o fantasma e tenta alcançar a pessoa.
- **Jogador 2 (Person):** controla a pessoa e deve fugir até o fim do tempo.

O mapa é um labirinto fixo de **32 × 16 células** (16 px por célula), com paredes, corredores e limites de tela. Ambos os personagens são posicionados aleatoriamente em células livres e não podem atravessar paredes. A pessoa começa com uma vantagem de **3 segundos**, durante os quais o fantasma fica parado. Depois disso, a perseguição dura até o cronômetro atingir **63 segundos**.

## Regras

- Se o fantasma tocar a pessoa, **Ghost vence**.
- Se o tempo se esgotar sem a captura, **Person vence**.
- Ao final, a mensagem aparece no centro da tela e o jogo reinicia automaticamente.
- Pressionar `Esc` encerra a partida; na tela final, pressione `Esc` novamente (após soltar a tecla) para sair.

## Controles

| Ação | Jogador 1 (Ghost) | Jogador 2 (Person) |
| --- | --- | --- |
| Mover para cima | `↑` | `W` / `w` |
| Mover para baixo | `↓` | `S` / `s` |
| Mover para a esquerda | `←` | `A` / `a` |
| Mover para a direita | `→` | `D` / `d` |
| Parar | `P` | `P` |

Qualquer tecla inicia o jogo na tela de abertura. Ao receber uma direção, o personagem se move automaticamente até encontrar uma parede ou até que `P` seja pressionado.

## Requisitos

- Ferramentas oficiais do [nand2tetris](https://www.nand2tetris.org/software): `JackCompiler` e `VMEmulator`.
- Java disponível para executar as ferramentas do nand2tetris.

## Como executar

1. Compile os arquivos Jack:

   ```bash
   "<caminho-do-nand2tetris>/tools/JackCompiler.sh" src
   ```

   Os arquivos `.vm` gerados ficam junto dos `.jack` em `src/`.

2. Abra o **VMEmulator**.
3. Selecione `src` como diretório do programa.
4. Carregue o programa e clique em **Run**.

## Estrutura do projeto

```text
Ghost-Multiplayer/
├── docs/
│   ├── Projeto 6.pdf
│   └── resumo_elementos_computacionais.pdf
├── src/
│   ├── Ghost.jack       # sprite, desenho e movimentação do fantasma
│   ├── GhostGame.jack   # estado do jogo, entradas, colisão, tempo e tela final
│   ├── Main.jack        # inicialização, reinício e encerramento
│   ├── Maze.jack        # layout do labirinto, desenho e colisão com paredes
│   ├── Person.jack      # sprite, desenho e movimentação da pessoa
│   └── Random.jack      # gerador pseudoaleatório usado nas posições iniciais
├── LICENSE
└── README.md
```

## Decisões de implementação

- A movimentação é contínua após uma única tecla de direção, evitando conflitos de teclado entre os dois jogadores.
- A colisão com paredes é feita convertendo a posição em pixels para índice no mapa.
- A colisão entre jogadores compara as posições em células do fantasma e da pessoa.
- O atraso de 3 segundos é implementado com contagem de ciclos, sem bloquear o loop principal do jogo.
- O cronômetro é atualizado no canto superior esquerdo da tela.

## Documentação

- [Especificação do Projeto 6](<docs/Projeto 6.pdf>)
- [Resumo de Elementos de Sistemas Computacionais](<docs/resumo_elementos_computacionais.pdf>)

## Licença

Distribuído sob a licença Apache License 2.0. Veja `LICENSE`.
