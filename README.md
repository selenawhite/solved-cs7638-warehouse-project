Download Link: https://assignmentchef.com/product/solved-cs7638-warehouse-project
<br>
Your file must be called warehouse.py and must have two classes called DeliveryPlanner_PartA and DeliveryPlanner_PartB.

<ul>

 <li>You may add additional classes and functions as needed provided they are all in this file warehouse.py.</li>

 <li>You may share code between partA and partB but it MUST BE IN THE FILE ‘warehouse.py’</li>

 <li>Your submission will consist of the warehouse.py file (only) which will be uploaded to Gradescope. Do not archive (zip,tar,etc) it.</li>

 <li>Your code must be valid python version 3 code</li>

 <li>You may use the numpy library.</li>

 <li>Your warehouse.py file must not execute any code when imported.</li>

 <li>Ask any questions about the directions or specifications on Piazza.</li>

</ul>

<h1>Part A</h1>

In this Part A, you will build a planner that helps a robot find the best path through a warehouse filled with boxes that it has to pick up and deliver to a dropzone.

DeliveryPlanner_PartA must have an __init__ function that takes three arguments: self, warehouse, and todo. DeliveryPlanner_PartA must also have a function called plan_delivery that takes a single argument: self.

<h2>Part A Input Specifications</h2>

warehouse will be a list of m strings, each with n characters, corresponding to the layout of the warehouse. The warehouse is an m x n grid. warehouse[i][j] corresponds to the spot in the ith row and jth column of the warehouse, where the 0th row is the northern end of the warehouse and the 0th column is the western end.

The characters in each string will be one of the following:

. (period) : traversable space. The robot may enter from any adjacent space.

# (hash) : a wall. The robot cannot enter this space.

@ (dropzone) : the starting point for the robot and the space where all boxes must be delivered. The dropzone may be traversed like a . space.

[0-9a-zA-Z] (any alphanumeric character) : a box. At most one of each alphanumeric character will be present in the warehouse (meaning there will be at most 62 boxes). A box may not be traversed, but if the robot is adjacent to the box, the robot can pick up the box. Once the box has been removed, the space functions as a . space.

<strong>Note</strong>: Test cases in the test suite will only contain the characters listed above. There is a helper function

(_set_initial_state_from) that parses this initial input into an internal warehouse state. Note that this is the same internal state representation that is used by the testing suite. You are not required to use this helper function, it is just provided for convenience. The helper function includes one additional character denoting the location of the robot:

* (asterisk) : the current location of the robot. When the current location of the robot is the same as the dropzone then the warehouse cell will be * instead of @. For example,

warehouse = [‘1#2’, ‘.#.’,

‘<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="7e50503e">[email protected]</a>’]

is a 3×3 warehouse.

<ul>

 <li>The dropzone is at the warehouse cell in row 2, column 2.</li>

 <li>Box 1 is located in the warehouse cell in row 0, column 0.</li>

 <li>Box 2 is located in the warehouse cell in row 0, column 2.</li>

 <li>There are walls in the warehouse cells in row 0, column 1 and row 1, column 1.</li>

 <li>The remaining five warehouse cells contain empty space. (The dropzone is empty space)</li>

 <li>After this warehouse is parsed using the helper function (_set_initial_state_from), the @ will be replaced with a * because the robot’s starting location is the dropzone. The testing suite has its’ own copy of the warehouse state used to execute your delivery plan to check for success. In the testing suite, after the robot moves out of the dropzone cell, the dropzone is denoted with the @ again. You are free to continue with this convention in your code, or choose another convention of keeping track of the robot, dropzone, walls, and boxes. Either way, you must update your internal warehouse state in your code as this is not done for you.</li>

</ul>

The argument todo is a list of alphanumeric characters giving the order in which the boxes must be delivered to the dropzone. For example, if todo = [‘1′,’2’] is given with the above example warehouse, then the robot must first deliver box 1 to the dropzone, and then the robot must deliver box 2 to the dropzone.

<h2>Part A Rules for Movement</h2>

<ul>

 <li>Two spaces are considered adjacent if they share an edge or a corner.</li>

 <li>The robot may move horizontally or vertically at a cost of 2 per move.</li>

 <li>The robot may move diagonally at a cost of 3 per move.</li>

 <li>The robot may not move outside the warehouse.</li>

 <li>The warehouse does not “wrap” around.</li>

 <li>As described earlier, the robot may pick up a box that is in an adjacent square.</li>

 <li>The cost to pick up a box is 4, regardless of the direction the box is relative to the robot.</li>

 <li>While holding a box, the robot may not pick up another box.</li>

 <li>The robot may put a box down on an adjacent empty space (.) or the dropzone (@) at a cost of 2 (regardless of the direction in which the robot puts down the box).</li>

 <li>If a box is placed on the @ space, it is considered delivered and is removed from the warehouse.</li>

 <li>The warehouse will be arranged so that it is always possible for the robot to move to the next box on the todo list without having to rearrange any other boxes.</li>

</ul>

An illegal move will incur a cost of 100, and the robot will not move (the standard costs for a move will not be additionally incurred). Illegal moves include:

<ul>

 <li>attempting to move to a nonadjacent, nonexistent, or occupied space</li>

 <li>attempting to pick up a nonadjacent or nonexistent box</li>

 <li>attempting to pick up a box while holding one already</li>

 <li>attempting to put down a box on a nonadjacent, nonexistent, or occupied space (this means the robot may not drop a box on the drop zone while the robot is occupying the drop zone) • attempting to put down a box while not holding one</li>

</ul>

<h2>Part A Output Specifications</h2>

plan_delivery should return a LIST of moves that minimizes the total cost of completing the task successfully. Each move should be a string formatted as follows:

<ul>

 <li>‘move {d}’, where ‘{d}’ is replaced by the direction the robot will move:</li>

</ul>

“n”, “e”, “s”, “w”, “ne”, “se”, “nw”, “sw”

<ul>

 <li>‘lift {x}’, where ‘{x}’ is replaced by the alphanumeric character of the box being picked up • ‘down {d}’, where ‘{d}’ is replaced by the direction the robot will put down the box:</li>

</ul>

“n”, “e”, “s”, “w”, “ne”, “se”, “nw”, “sw”

For example, for the values of warehouse and todo given previously (reproduced below):

warehouse = [‘1#2’, ‘.#.’,

‘<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="311f1f71">[email protected]</a>’]

todo = [‘1′,’2’] plan_delivery might return the following:

[‘move w’,

‘move nw’,

‘lift 1’,

‘move se’,

‘down e’,

‘move ne’,

‘lift 2’,

‘down s’]

<h1>Part B</h1>

In this Part B, you will build a planner that helps a robot find the best path through a warehouse to a single box that it has to pick up and deliver to a dropzone. This part differs from part A, in that there is a single box, but now the warehouse has an “uneven” floor that imposes an additional, positive, cost on each robot command. In addition, the robot may “wake up” at any point in the warehouse and be tasked with retrieving the box and delivering it to the dropzone. Because of this, this project is most easily solved using the dynamic programming approach covered in Lesson 12: 14-19 and problem set 4, question 5.

DeliveryPlanner_PartB must have an __init__ function that takes three arguments: self, warehouse, warehouse_cost, and todo. DeliveryPlanner_PartB must also have a function called plan_delivery that takes the argument, self and a flag debug set to default to False.

<h2>Part B Input Specifications</h2>

warehouse will be a list of m strings, each with n characters, corresponding to the layout of the warehouse. The warehouse is an m x n grid. warehouse[i][j] corresponds to the spot in the ith row and jth column of the warehouse, where the 0th row is the northern end of the warehouse and the 0th column is the western end.

The characters in each string will be one of the following:

. (period) : traversable space. The robot may enter from any adjacent space.

# (hash) : a wall. The robot cannot enter this space.

@ (dropzone): the starting point for the robot and the space where all boxes must be delivered. The dropzone may be traversed like a . space.

1 : the single box to be retrieved. A box may not be traversed, but if the robot is adjacent to the box, the robot can pick up the box. Once the box has been removed, the space functions acts as a . space. For example:

warehouse = [‘1..’, ‘.#.’,

‘<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="527c7c12">[email protected]</a>’]

is a 3×3 warehouse.

<ul>

 <li>The dropzone is at the warehouse cell in row 2, column 2.</li>

 <li>Box 1 is located in the warehouse cell in row 0, column 0.</li>

 <li>There is a wall in the warehouse cells in row 1, column 1.</li>

 <li>The remaining six warehouse cells contain empty space. (The dropzone is also empty space)</li>

</ul>

The argument warehouse_cost is a list of lists such that indices i,j refer to the positive cost at the row i and column j in the warehouse. For the case above, the corresponding warehouse_cost could be:

warehouse_cost = [[ 0,                                5, 2],

[10, math.inf, 2],

[ 2,                     10, 2]]

where the interior “wall” has cost=infinity.

The argument todo is a list of alphanumeric characters giving the order in which the boxes must be delivered to the dropzone. For part B this is limited to a single box as follows:

todo = [‘1’] which indicates that box 1 must be retrieved and delivered to the dropzone.

Note: todo is kept consistent with part A for convenience and possible future expansion of the project requirements.

There is no input for initial robot location because the robot may “wake up” at any point in the warehouse and must be handed a “policy” so that no matter where it is, it can retrieve the box. Further, because it may lift the box from different squares depending on its starting location, it requires another “policy” to deliver the box to the dropzone.

<strong>Part B Rules for Movement</strong>

Rules for Movement are the same as those for part A. Please refer to part A documentation.

<h2>Part B Output Specifications</h2>

plan_delivery should return two policies, each as a LIST of LISTs of strings indicating the command at each square on the grid. The format of the commands is the same as in part A. The special command ‘-1’ should be placed at any square for which there is no valid command, such as a wall.

For example, for the values of warehouse and todo given previously (reproduced below):

warehouse = [‘1..’, ‘.#.’,

‘<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="f9d7d7b9">[email protected]</a>’]

todo = [‘1’] plan_delivery might return the following two policies: To Box Policy:

[[‘B’        , ‘lift 1’ , ‘move w’ ] [‘lift 1’, ‘-1’ , ‘move nw’]

[‘move n’, ‘move nw’, ‘move n’ ]]

Deliver Box Policy:

[[‘move e’ , ‘move se’, ‘move s’] [‘move ne’,  ‘-1’ , ‘down s’]

[‘move e’ , ‘down e’ , ‘move n’]]

where: ‘B’ indicates the box location. ‘-1’ indicates a square with no command

For the case of the “Deliver Box Policy”, the dropzone includes the optimal move out of it in the event the robot starts on, lifts an adjacent box, and then must move off the dropzone to deliver it.

The testing suite will pick a starting location for the robot and then execute the appropriate moves in the

“To Box Policy” until it finds and lifts the box with a lift 1 command. At this point execution transitions to the “Deliver Box Policy” and, given the location of the robot when it lifted the box, the appropriate commands are executed until the the box is delivered to the dropzone.

<h1>Environment Test</h1>

Before changing warehouse.py, test your environment in three steps:

<ul>

 <li>From the command line type: python warehouse.py

  <ul>

   <li>list of moves for Part A test case 1 should be printed</li>

  </ul></li>

</ul>

A “to_box_policy” and “deliver_policy” will be printed for part B, test case 1

<ul>

 <li>From the command line type: python testing_suite_PartA.py

  <ul>

   <li>list of test cases and their score should show that test case 1 passed and the remaining failed. Thereare more notes in testing_suite_partA.py to discuss how to run and debug it</li>

  </ul></li>

 <li>From the command line type: python testing_suite_PartB.py

  <ul>

   <li>list of test cases and their score should show that test case 1 passed and the remaining failed. Thereare more notes in testing_suite_partB.py to discuss how to run and debug it</li>

  </ul></li>

</ul>

<h1>Development and Debugging</h1>

When developing and debugging here are some ideas that might prove helpful.

<ul>

 <li>During initial development of your algorithm use warehouse.py and its main function

  <ul>

   <li>Copy a test case from the testing suite to the <strong><sub>main </sub></strong>in the bottom of warehouse.py</li>

   <li>To run from the command line type: python warehouse.py or run in your IDE such as pycharm</li>

   <li>Make sure code executes without errors</li>

   <li>Check the output, moves (for part A) and policy (for part B)</li>

  </ul></li>

 <li>Test your algorithm using testing_suite_partA.py or testing_suite_partB.py

  <ul>

   <li>You can run a single test case. For example to run the first test case for partA:</li>

  </ul></li>

</ul>

python testing_suite_partA.py PartATestCase.test_case1

<ul>

 <li>Or you may comment out all but a single test case in the testing_suite</li>

</ul>

<ul>

 <li>If testing in a debugger, to allow breakpoints to work properly, there are some flags that can be set at the top of testing_suite_partA.py and testing_suite_partB.py

  <ul>

   <li>Set the flag TIME_OUT to a very large value (like 600 seconds)</li>

   <li>Set flag DEBUGGING_SINGLE_PROCESS = True ( this disables multiprocess which messes with most debuggers</li>

   <li>Set the flag VERBOSE_FLAG = True

    <ul>

     <li>provides a simple console based visualization</li>

     <li>if exceptions are raised provides detailed stack trace</li>

    </ul></li>

   <li>After the test case of interest works be sure to set the flags back

    <ul>

     <li>VERBOSE_FLAG = False</li>

     <li>TIME_OUT = 5</li>

     <li>DEBUGGING_SINGLE_PROCESS = False</li>

    </ul></li>

  </ul></li>

</ul>