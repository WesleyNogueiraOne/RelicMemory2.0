# 📖 RelicMemory - Plugin de Memórias Imersivas

RelicMemory é um plugin de Spigot para Minecraft focado em storytelling e imersão. Ele permite que administradores de servidores criem "memórias" em locais específicos do mundo, que são ativadas quando um jogador passa pela área carregando um item especial — uma "Relíquia".

Ao ser ativada, a memória desencadeia uma sequência cinematográfica totalmente personalizável com títulos na tela, mensagens no chat, sons, partículas e até mesmo a execução de comandos de outros plugins, criando eventos de lore, quests e experiências únicas para os jogadores.

## ✨ Funcionalidades

-   **Relíquias Customizáveis:** Crie quantos itens especiais quiser, definindo seu material, nome, descrição e um ID único.
-   **Zonas de Memória 3D:** Defina áreas tridimensionais no mundo que servem como gatilho para as memórias.
-   **Sequenciador de Ações:** Crie "cinematics" detalhadas com uma lista simples de ações, controlando o ritmo com atrasos para máximo impacto.
-   **Sistema de Cooldown:** Evite que as memórias sejam ativadas repetidamente, configurando um tempo de recarga para cada uma.
-   **Gerenciamento In-Game:** Crie e configure quase todos os aspectos do plugin (relíquias, locais, links) diretamente do jogo, sem precisar editar os arquivos manualmente.
-   **Integração com Outros Plugins:** Execute comandos de outros plugins como parte da sua sequência de memória, permitindo uma integração poderosa (ex: iniciar um evento, dar uma recompensa, etc.).

---

## 🎮 Comandos

A administração do plugin é dividida em um comando para jogadores (`/getrelic`) e um comando geral para admins (`/rm` ou `/relicmemory`).

### Comando de Jogador

| Comando                       | Descrição                                 | Permissão              |
| ----------------------------- | ----------------------------------------- | ---------------------- |
| `/getrelic <id_da_reliquia>` | Entrega ao jogador a relíquia especificada. | `relicmemory.getrelic` |

### Comandos de Administrador (`/rm`)

| Comando                                        | Descrição                                                                                             | Permissão                      |
| ---------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ------------------------------ |
| `/rm wand`                                     | Entrega a "Varinha de Seleção" para marcar os cantos da zona de memória.                              | `relicmemory.admin.wand`       |
| `/rm define <id_da_memoria>`                   | Salva a área selecionada como uma nova memória com o ID especificado.                                   | `relicmemory.admin.define`     |
| `/rm createrelic <id_da_reliquia> <material>`  | Cria a base de uma nova relíquia no `config.yml`.                                                      | `relicmemory.admin.createrelic`|
| `/rm setrelic name <id> <nome...>`             | Define o nome de exibição de uma relíquia (suporta códigos de cor `&`).                                  | `relicmemory.admin.setrelic`   |
| `/rm setrelic lore add <id> <linha...>`        | Adiciona uma linha à descrição (lore) de uma relíquia.                                                | `relicmemory.admin.setrelic`   |
| `/rm setmemory <id_memoria> relic add <id_reliquia>` | Vincula uma relíquia a uma memória, tornando-a necessária para a ativação.                           | `relicmemory.admin.setmemory`  |

---

## ⚙️ Configuração (`config.yml`)

Embora a maior parte da configuração possa ser feita in-game, a criação das sequências cinematográficas é feita no arquivo `config.yml`.

### Estrutura Geral

```yaml
# Seção para definir todos os tipos de relíquias.
relics:
  espada_heroi:
    material: 'IRON_SWORD'
    name: '&cLâmina Gasta do Herói'
    lore:
      - '&7Mesmo quebrada, ainda ressoa com'
      - '&7ecos de batalhas passadas.'
# Seção para definir todas as memórias.
memories:
  ruina_do_heroi:
    world: 'world'
    pos1: {x: 100, y: 65, z: 200}
    pos2: {x: 110, y: 70, z: 210}
    cooldown: 60
    required-relics:
      - 'espada_heroi'
    actions:
      # A sua sequência cinematográfica vai aqui!
      - 'SOUND: BLOCK_BELL_RESONATE'
      - 'TITLE: &7A lâmina em sua mão... | &f...começa a tremer.'
      - 'DELAY: 60'
      - 'CMD: cvevent start meteor'
