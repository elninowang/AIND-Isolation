
# Build a Game-playing Agent 建立一个游戏代理

![Example game of isolation](viz.gif)

## Synopsis 概要

In this project, students will develop an adversarial search agent to play the game "Isolation".  Isolation is a deterministic, two-player game of perfect information in which the players alternate turns moving a single piece from one cell to another on a board.  Whenever either player occupies a cell, that cell becomes blocked for the remainder of the game.  The first player with no remaining legal moves loses, and the opponent is declared the winner.  These rules are implemented in the `isolation.Board` class provided in the repository. 

在这个项目中，学生将开发一种对抗性搜索代理玩“隔离”游戏。隔离是确定性的，双人游戏的完美信息，其中玩家交替转动将单个单元从一个单元移动到另一个单元。每当任何一个玩家占据一个单元格，该游戏的剩余部分就会被阻止。没有剩余法律诉讼的第一名球员失败，对手被宣布为胜利者。这些规则在存储库中提供的`isolation.Board`类中实现。

This project uses a version of Isolation where each agent is restricted to L-shaped movements (like a knight in chess) on a rectangular grid (like a chess or checkerboard).  The agents can move to any open cell on the board that is 2-rows and 1-column or 2-columns and 1-row away from their current position on the board. Movements are blocked at the edges of the board (the board does not wrap around), however, the player can "jump" blocked or occupied spaces (just like a knight in chess).

该项目使用一个版本的隔离，每个代理限制在矩形网格（如棋牌或棋盘）上的L形运动（像象棋中的骑士）。代理可以移动到板上任何离开当前位置的2行和1列或2列和1行的任何开放单元格。移动在板的边缘被阻挡（板不会缠绕），但是玩家可以“跳”阻塞或占用空间（就像骑士在国际象棋中）。

Additionally, agents will have a fixed time limit each turn to search for the best move and respond.  If the time limit expires during a player's turn, that player forfeits the match, and the opponent wins.

此外，代理将有一个固定的时间限制，以搜索最好的举动和回应。如果时间限制在玩家回合期间过期，该玩家将丧失比赛，并且对手获胜。

Students only need to modify code in the `game_agent.py` file to complete the project.  Additional files include example Player and evaluation functions, the game board class, and a template to develop local unit tests.  

学生只需要修改`game_agent.py`文件中的代码即可完成该项目。附加文件包括播放器和评估功能的示例，游戏板类，以及开发本地单元测试的模板。

## Instructions 说明

In order to complete the Isolation project, students must submit code that passes all test cases for the required functions in `game_agent.py` and complete a report as specified in the rubric.  Students can submit using the [Udacity Project Assistant]() command line utility.  Students will receive feedback on test case success/failure after each submission.

为了完成隔离项目，学生必须提交代码，通过`game_agent.py`中所需功能的所有测试用例，并按照规格完成报告。学生可以使用 [Udacity Project Assistant]() 命令行实用程序提交。每次提交后，学生将收到关于测试用例成功/失败的反馈。

Students must implement the following functions:

学生必须实施以下功能：

- `MinimaxPlayer.minimax()`: implement minimax search
- `AlphaBetaPlayer.alphabeta()`: implement minimax search with alpha-beta pruning
- `AlphaBetaPlayer.get_move()`: implement iterative deepening search
- `custom_score()`: implement your own best position evaluation heuristic
- `custom_score_2()`: implement your own alternate position evaluation heuristic
- `custom_score_3()`: implement your own alternate position evaluation heuristic

- `MinimaxPlayer.minimax()`: 实现minimax搜索
- `AlphaBetaPlayer.alphabeta()`: 使用alpha-beta 修剪实现最小值搜索
- `AlphaBetaPlayer.get_move()`: 实现迭代深化搜索
- `custom_score()`: 实现你自己的最佳位置评估启发式
- `custom_score_2()`: 实现你自己的备用位置评估启发式
- `custom_score_3()`: 实现你自己的备用位置评估启发式

You may write or modify code within each file (but you must maintain compatibility with the function signatures provided).  You may add other classes, functions, etc., as needed, but it is not required.

您可以在每个文件中编写或修改代码（但必须保持与提供的功能签名的兼容性）。您可以根据需要添加其他类，功能等，但不是必需的。

The Project Assistant sandbox for this project places some restrictions on the modules available and blocks calls to some of the standard library functions.  In general, standard library functions that introspect code running in the sandbox are blocked, and the PA only allows the following modules `random`, `numpy`, `scipy`, `sklearn`, `itertools`, `math`, `heapq`, `collections`, `array`, `copy`, and `operator`. (Modules within these packages are also allowed, e.g., `numpy.random`.)

该项目的项目助理沙箱对可用的模块有一些限制，并阻止对某些标准库函数的调用。一般来说，标准库函数会阻止在沙箱中运行的代码，PA只允许以下模块  `random`, `numpy`, `scipy`, `sklearn`, `itertools`, `math`, `heapq`, `collections`, `array`, `copy`, 和 `operator`。 （也可以使用这些软件包中的模块，例如`numpy.random`）。

### Quickstart Guide 快速入门指南

The following example creates a game and illustrates the basic API.  You can run this example by activating your aind anaconda environment and executing the command `python sample_players.py`

以下示例创建一个游戏并说明了基本的API。 您可以通过激活aind anaconda环境并执行命令 `python sample_players.py` 来运行此示例

    from isolation import Board
    from sample_players import RandomPlayer
    from sample_players import GreedyPlayer

    # create an isolation board (by default 7x7)
    player1 = RandomPlayer()
    player2 = GreedyPlayer()
    game = Board(player1, player2)

    # place player 1 on the board at row 2, column 3, then place player 2 on
    # the board at row 0, column 5; display the resulting board state.  Note
    # that the .apply_move() method changes the calling object in-place.
    game.apply_move((2, 3))
    game.apply_move((0, 5))
    print(game.to_string())

    # players take turns moving on the board, so player1 should be next to move
    assert(player1 == game.active_player)

    # get a list of the legal moves available to the active player
    print(game.get_legal_moves())

    # get a successor of the current state by making a copy of the board and
    # applying a move. Notice that this does NOT change the calling object
    # (unlike .apply_move()).
    new_game = game.forecast_move((1, 1))
    assert(new_game.to_string() != game.to_string())
    print("\nOld state:\n{}".format(game.to_string()))
    print("\nNew state:\n{}".format(new_game.to_string()))

    # play the remainder of the game automatically -- outcome can be "illegal
    # move", "timeout", or "forfeit"
    winner, history, outcome = game.play()
    print("\nWinner: {}\nOutcome: {}".format(winner, outcome))
    print(game.to_string())
    print("Move history:\n{!s}".format(history))


### Coding 写代码

The steps below outline a suggested process for completing the project -- however, this is just a suggestion to help you get started.  A stub for writing unit tests is provided in the `agent_test.py` file (no local test cases are provided). (See the [unittest](https://docs.python.org/3/library/unittest.html#basic-example) module for information on getting started.)

下面的步骤概述了完成项目的建议过程 - 但这只是一个帮助您开始的建议。`agent_test.py` 文件中提供了一个用于编写单元测试的存根（没有提供本地测试用例）。 （有关入门信息，请参阅  [unittest](https://docs.python.org/3/library/unittest.html#basic-example) 模块。）

The primary mechanism for testing your code will be the Udacity Project Assistant command line utility.  You can install the Udacity-PA tool by activating your aind anaconda environment, then running `pip install udacity-pa`.  You can submit your code for scoring by running `udacity submit isolation`.  The project assistant server has a collection of unit tests that it will execute on your code, and it will provide feedback on any successes or failures.  You must pass all test cases in the project assistant before you can complete the project by submitting your report for review.

用于测试代码的主要机制将是Udacity Project Assistant命令行实用程序。您可以通过激活您的aind anaconda环境，然后运行`pip install udacity-pa`来安装Udacity-PA工具。您可以通过运行`udacity提交隔离'提交您的代码进行计分。项目助理服务器具有将在代码上执行的单元测试的集合，并且将为任何成功或失败提供反馈。您必须通过项目助手中的所有测试用例，然后才能通过提交报告来完成项目审核。

0. Verify that the Udacity-PA tool is installed properly by submitting the project. Run `udacity submit isolation`. (You should see a list of test cases that failed -- that's expected because you haven't implemented any code yet.)

通过提交项目，验证Udacity-PA工具是否正确安装。运行`udacity提交隔离'。 （您应该看到失败的测试用例列表 - 预计是因为尚未实现任何代码。）

0. Modify the `MinimaxPlayer.minimax()` method to return any legal move for the active player.  Resubmit your code to the project assistant and the minimax interface test should pass.

修改 `MinimaxPlayer.minimax()` 方法返回活动播放器的任何合法移动。将代码重新提交给项目助理，并且最小化接口测试应该通过。

0. Further modify the `MinimaxPlayer.minimax()` method to implement the full recursive search procedure described in lecture (ref. [AIMA Minimax Decision](https://github.com/aimacode/aima-pseudocode/blob/master/md/Minimax-Decision.md)).  Resubmit your code to the project assistant and both the minimax interface and functional test cases will pass.

进一步修改 `MinimaxPlayer.minimax()` 方法来实现演讲中描述的完整的递归搜索过程（参考文献 [AIMA Minimax Decision](https://github.com/aimacode/aima-pseudocode/blob/master/md/Minimax-Decision.md)）。将代码重新提交给项目助理，最小化接口和功能测试用例将通过。

0. Start on the alpha beta test cases. Modify the `AlphaBetaPlayer.alphabeta()` method to return any legal move for the active player.  Resubmit your code to the project assistant and the alphabeta interface test should pass.

从alpha beta测试开始。修改 `AlphaBetaPlayer.alphabeta()` 方法以返回活动播放器的任何合法移动。重新提交你的代码到项目助理和字母表接口测试应该通过。

0. Further modify the `AlphaBetaPlayer.alphabeta()` method to implement the full recursive search procedure described in lecture (ref. [AIMA Alpha-Beta Search](https://github.com/aimacode/aima-pseudocode/blob/master/md/Alpha-Beta-Search.md)).  Resubmit your code to the project assistant and both the alphabeta interface and functional test cases will pass.

进一步修改 `AlphaBetaPlayer.alphabeta()` 方法来实现演讲中描述的完整的递归搜索过程（参考文献[AIMA Alpha-Beta Search](https://github.com/aimacode/aima-pseudocode/blob/master/md/Alpha-Beta-Search.md) ）。将代码重新提交给项目助理，字母表界面和功能测试用例将通过。

0. You can pass the interface test for the `AlphaBetaPlayer.get_move()` function by copying the code from `MinimaxPlayer.get_move()`.  Resubmit your code to the project assistant to see that the `get_move()` interface test case passes.

通过复制 `MinimaxPlayer.get_move()` 中的代码，可以传递 `AlphaBetaPlayer.get_move()` 函数的接口测试。重新提交你的代码到项目助理看到`get_move()` 接口测试用例通过。

0. Pass the test_get_move test by modifying `AlphaBetaPlayer.get_move()` to implement Iterative Deepening.  See Also [AIMA Iterative Deepening Search](https://github.com/aimacode/aima-pseudocode/blob/master/md/Iterative-Deepening-Search.md)

通过修改 `AlphaBetaPlayer.get_move()` 来执行test_get_move测试来实现迭代深化。另请参阅 [AIMA迭代深化搜索](https://github.com/aimacode/aima-pseudocode/blob/master/md/Iterative-Deepening-Search.md)

0. Finally, pass the heuristic tests by implementing any heuristic in `custom_score()`, `custom_score_2()`, and `custom_score_3()`.  (These test cases only validate the return value type -- it does not check for "correctness" of your heuristic.)  You can see example heuristics in the `sample_players.py` file.

最后，通过在 `custom_score()`, `custom_score_2()`, 和 `custom_score_3()` 中实现任何启发式来传递启发式测试。 （这些测试用例仅验证返回值类型 - 它不会检查您的启发式的“正确性”。）您可以在 `sample_players.py` 文件中看到示例启发式。

### Tournament 比赛

The `tournament.py` script is used to evaluate the effectiveness of your custom heuristics.  The script measures relative performance of your agent (named "Student" in the tournament) in a round-robin tournament against several other pre-defined agents.  The Student agent uses time-limited Iterative Deepening along with your custom heuristics.

`tournament.py'脚本用于评估您的自定义启发式的有效性。脚本在与其他预定义代理程序的循环赛中测量您的代理（在比赛中名为“学生”）的相对性能。学生代理使用时间限制迭代深化以及您的自定义启发式。

The performance of time-limited iterative deepening search is hardware dependent (faster hardware is expected to search deeper than slower hardware in the same amount of time).  The script controls for these effects by also measuring the baseline performance of an agent called "ID_Improved" that uses Iterative Deepening and the improved_score heuristic defined in `sample_players.py`.  Your goal is to develop a heuristic such that Student outperforms ID_Improved. (NOTE: This can be _very_ challenging!)

时间有限的迭代深化搜索的性能是硬件依赖的（更快的硬件预计在相同的时间内比较慢的硬件搜索更深）。脚本通过测量使用迭代深化的代理名为“ID_Improved”的代理和 `sample_players.py` 中定义的改进的启发式启发法来控制这些效果。您的目标是开发一个启发式，使得学生优于ID_Improved。 （注意：这可能是_very_具有挑战性！）

The tournament opponents are listed below. (See also: sample heuristics and players defined in sample_players.py)

- Random: An agent that randomly chooses a move each turn.
- MM_Open: MinimaxPlayer agent using the open_move_score heuristic with search depth 3
- MM_Center: MinimaxPlayer agent using the center_score heuristic with search depth 3
- MM_Improved: MinimaxPlayer agent using the improved_score heuristic with search depth 3
- AB_Open: AlphaBetaPlayer using iterative deepening alpha-beta search and the open_move_score heuristic
- AB_Center: AlphaBetaPlayer using iterative deepening alpha-beta search and the center_score heuristic
- AB_Improved: AlphaBetaPlayer using iterative deepening alpha-beta search and the improved_score heuristic

比赛对手列在下面。 （另见：sample_players.py中定义的样本启发式和玩家）

- Random：每轮随机选择一个动作的代理。
- MM_Open：MinimaxPlayer代理使用open_move_score启发式搜索深度3
- MM_Center：MinimaxPlayer代理使用center_score启发式搜索深度3
- MM_改进：MinimaxPlayer代理使用改进后的启发式搜索深度3
- AB_Open：AlphaBetaPlayer使用迭代深化alpha-beta搜索和open_move_score启发式
- AB_Center：AlphaBetaPlayer使用迭代深化alpha-beta搜索和center_score启发式
- AB_改进：AlphaBetaPlayer使用迭代深化alpha-beta搜索和改进的评估启发式

## Submission 提交

Before submitting your solution to a reviewer, you are required to submit your project to Udacity's Project Assistant, which will provide some initial feedback.

在将解决方案提交给审阅者之前，您需要将项目提交给Udacity的项目助理，这将提供一些初步的反馈。

Please see the instructions in the [AIND-Sudoku](https://github.com/udacity/AIND-Sudoku#submission) project repository for installation and setup instructions. 

请参阅 [AIND-Sudoku](https://github.com/udacity/AIND-Sudoku#submission) 项目存储库中有关安装和设置说明的说明。

To submit your code to the project assistant, run `udacity submit isolation` from within the top-level directory of this project. You will be prompted for a username and password. If you login using google or facebook, follow the [instructions for using a jwt](https://project-assistant.udacity.com/faq).

要将代码提交给项目助理，请在此项目的顶级目录中运行`udacity submit isolation`。 系统将提示您输入用户名和密码。 如果您使用Google或Facebook登录，请按照 [instructions for using a jwt](https://project-assistant.udacity.com/faq) 进行操作。

This process will create a zipfile in your top-level directory named `isolation-<id>.zip`. This is the file that you should submit to the Udacity reviews system.

此过程将在名为 `isolation-<id>.zip` 的顶级目录中创建一个zip文件。 这是您应该提交给Udacity评估系统的文件。


## Game Visualization 游戏可视化

The `isoviz` folder contains a modified version of chessboard.js that can animate games played on a 7x7 board.  In order to use the board, you must run a local webserver by running `python -m http.server 8000` from your project directory (you can replace 8000 with another port number if that one is unavailable), then open your browser to `http://localhost:8000` and navigate to the `/isoviz/display.html` page.  Enter the move history of an isolation match (i.e., the array returned by the Board.play() method) into the text area and run the match.  Refresh the page to run a different game.  (Feel free to submit pull requests with improvements to isoviz.)

`isoviz`文件夹包含一个修改版本的chessboard.js，可以在7x7板上弹奏游戏。 为了使用该板，您必须通过在项目目录中运行`python -m http.server 8000`来运行本地Web服务器（如果该目录不可用，则可以用另一个端口号代替8000），然后将浏览器打开为 `http://localhost:8000` 并导航到`/isoviz/display.html` 页面。 输入隔离匹配（即Board.play() 方法返回的数组）的移动历史记录到文本区域并运行匹配。 刷新页面以运行不同的游戏。 （随意改进isoviz提交拉请求。）

## PvP Competition PvP比赛

Once your project has been reviewed and accepted by meeting all requirements of the rubric, you are invited to complete the `competition_agent.py` file using any combination of techniques and improvements from lectures or online, and then submit it to compete in a tournament against other students from your cohort and past cohort champions.  Additional details (official rules, submission deadline, etc.) will be provided separately.

一旦您的项目通过满足标准的所有要求进行审查和接受，您将被邀请使用演讲或在线的任何技术和改进的组合来完成 `competition_agent.py`  文件，然后提交给竞争对手 其他学生从你的队列和过去的队列冠军。 额外的细节（官方规定，提交截止日期等）将另行提供。

The competition agent can be submitted using the Udacity project assistant:

竞争代理可以使用Udacity项目助理提交：

    udacity submit isolation-pvp
