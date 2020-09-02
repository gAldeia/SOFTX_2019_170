# SOFTX_2019_170 fork

Fork of GSGP-C++ 2.0: a Geometric Semantic Genetic Programming Framework. To refer to the original source code and publication, [click here](https://github.com/ElsevierSoftwareX/SOFTX_2019_170).

## Description

This fork is intented to extend some functionalities of the original source code by adding new function symbols: *{sqrt, tanh, exp, log, sin, cos}*.

Also, the fitness function was changed to the Root Mean Squared Error (RMSE), instead of using the Mean Absolute Error (MAE) as the original version.

## Modifications

The following functions were modifyied:

* GP.h file:
    * **parse_expression:** This function reads the file with the individuals and traces from the last run, to obtain the best expression. This is only used if the USE_TEST_SET option is configured in the configuration. NOTICE THAT if new symbols are created, we must treat them here in the parser, so that the reading and parse can be done without generating errors. As I created new symbols, I prefixed the character '\_' in all of them. I modified this part of the parser to recognize that when the parser finds a '\_', it is taking a symbol created by me. Unlike the symbols of the original functions, the ones I created are represented by a sctring with more than 1 character. Here I recognize which of the functions is being used, and use the index that I assigned to them at the time of creation (later) to create the corresponding node in the parser
    * **create_T_F:** Whenever I create a new one I need to increase the number that determines the size of the symbols array (original = 4). This functions creates the function symbols.
    * **print_math_style:** This function recognizes the node ID and decides how to print. Everything printed here must have a way of being treated in the parser.
    * **eval:** Here we must implement the computation that a symbol does over its children. All symbols that are created must have a way of being evaluated here. From that point down, they are the symbols that I created.If an operation can generate an error, make the implementation safe.
    * **Myevaluate:** This is the fitness function applied to expressions, FOR THE TRAINING PARTITION. Originally, the MAE was used. I made the change to be the RMSE.
    * **Myevaluate_test:** This is the fitness function applied to expressions, FOR THE TEST PARTITION. Originally, the MAE was used. I made the change to be the RMSE.
    * **update_training_fitness:** updates the training fitness, originally using the MAE. I changed to calculate the RMSE.
    * **update_test_fitness:** Same as the previous function, for the test partition.
* GP.cc file:
    * **main:** Commented the line that prints the generations.

## Disclaimer

This modification is distributed without warranty. At no time was there any intention to infringe the license or discredit the original authors. All modifications made to the original code are commented, indicating the author of the modification, the date on which it was made, and the desired objectives.

## License

This modified version is distributed under the same license *GNU AFFERO GENERAL PUBLIC LICENSE*, included in the github repository, and also available [here](https://www.gnu.org/licenses/#AGPL).