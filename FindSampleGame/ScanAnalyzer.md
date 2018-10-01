```csharp
//David McGinn
//10 - 1 - 18
//CMPS-4143
//ScanAnalyzer class consists of a resizeable grid,
//  stores two secret sample locations chosen
//  at random
//  keeps track of guesses, whether samples have been found
 


using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace FindSampleGame
{
    class ScanAnalyzer
    {
        private char[,] _grid;
        private int[] _sample1, _sample2; //stores x,y (column, row)
        private int _rows, _cols, _totGuesses, _curGuesses;
        private bool _found1, _found2;
        public int CurGuesses
        {
            get { return _curGuesses; }
        }

        //public ScanAnalyzer()
        //accepts int rows int cols and int guesses
        //calls PopulateArray() and HideSamples()
        //parameterized constructor
        public ScanAnalyzer(int rows, int cols, int guesses)
        {
            _grid = new char[rows, cols];
            _sample1 = new int[2];
            _sample2 = new int[2];
            _totGuesses = guesses;
            _curGuesses = 0;
            _found1 = false;
            _found2 = false;

            _rows = rows;
            _cols = cols;

            PopulateArray();
            HideSamples();
        }

        //public string DisplayGrid()
        //accepts no arguments
        //returns a string representation of _grid
        public string DisplayGrid()
        {
            string gridString = "";

            for(int r = 0; r < _rows; r++)
            {
                for(int c = 0; c < _cols; c++)
                {
                    gridString += _grid[r, c].ToString();
                    gridString += " ";
                }
                gridString += Environment.NewLine;
                gridString += Environment.NewLine;
            }

            return gridString;
        }

        //public bool GameWon()
        //accepts no arguments
        //returns a true if samples are found
        //false if they haven't been
        public bool GameWon()
        {
            if (_found1 && _found2)
                return true;
            return false;
        }

        //public bool GameOver()
        //accepts no argumenst
        //returns true if guesses have been used up
        //returns false if _curGuesses <= _totGuesses
        public bool GameOver()
        {
            if (_curGuesses >= _totGuesses)
                return true;
            return false;
        }

        //public bool EvaluateGuess()
        //Accepts int x, int y
        //returns true if sample is found
        //returns false if not
        //Updates _grid, if sample is discovered places a $
        //  if not places an appropriate arrow or -|
        //It guides to _sample1, then _sample2, otherwise the game would be
        //  super hard
        public bool EvaluateGuess(int x, int y, bool UDLR)
        {

            bool goodGuess = false;

            if (x > _grid.GetLength(1) - 1 || y > _grid.GetLength(0) - 1)
                throw new IndexOutOfRangeException("OB");
            else
            {
                //see if the guess is dead on for either sample
                if(x == _sample1[0] && y == _sample1[1])
                {
                    _grid[_sample1[1],_sample1[0]] = '$';
                    _found1 = true;
                }
                else if(x == _sample2[0] && y == _sample2[1])
                {
                    _grid[_sample2[1], _sample2[0]] = '$';
                    _found2 = true;
                }

                //if _sample1 is undiscovered guide to 1
                else if (!_found1)
                {
                    //guide vertical if UDLR == true
                    if (UDLR)
                    {
                        if (y > _sample1[1])
                        {
                            _grid[y, x] = '^';
                        }
                        else if (y < _sample1[1])
                        {
                            _grid[y, x] = 'V';
                        }
                        else if (y == _sample1[1])
                        {
                            _grid[y, x] = '-'; // if guess is in same row
                        }
                    }
                    
                    //guide horizontal if UDLR is false
                    else if (!UDLR)
                    {
                        if (x > _sample1[0])
                        {
                            _grid[y, x] = '<';
                        }
                        else if (x < _sample1[0])
                        {
                            _grid[y, x] = '>';
                        }
                        else if (x == _sample1[0])
                        {
                            _grid[y, x] = '|'; // if guess is in same column
                        }
                    }
                }
                //if _sample1 is discovered guide to _sample2
                else if (!_found2)
                {
                    //guide vertical if UDLR == true
                    if (UDLR)
                    {
                        if (y > _sample2[1])
                        {
                            _grid[y, x] = '^';
                        }
                        else if (y < _sample2[1])
                        {
                            _grid[y, x] = 'V';
                        }
                        else if (x == _sample2[1])
                        {
                            _grid[y, x] = '-'; // if guess is in same row
                        }
                    }

                    //guide horizontal if UDLR is false
                    else if (!UDLR)
                    {
                        if (x > _sample2[0])
                        {
                            _grid[y, x] = '<';
                        }
                        else if (x < _sample2[0])
                        {
                            _grid[y, x] = '>';
                        }
                        else if (x == _sample2[0])
                        {
                            _grid[y, x] = '|'; // if guess is in same column
                        }
                    }
                }
            }

            _curGuesses++;
            return goodGuess;
        }

        //private void PopulateArray
        //called ONLY by constructor to populate _grid
        private void PopulateArray()
        {
            for(int r = 0; r < _rows; r++)
            {
                for(int c = 0; c < _cols; c++)
                {
                    _grid[r, c] = '~';
                }
            }
        }

        //private void HideSamples()
        //called ONLY by constructor to hide samples
        private void HideSamples()
        {
            Random r = new Random();

            //_grid.GetLength(0) gets number of rows(first dimension)
            //_grid.GetLength(1) gets number of columns(second dimension)
            _sample1[0] = r.Next(_grid.GetLength(1));
            _sample1[1] = r.Next(_grid.GetLength(0));

            //ensure samples aren't placed in the same spot
            do
            {
                _sample2[0] = r.Next(_grid.GetLength(1));
                _sample2[1] = r.Next(_grid.GetLength(0));
            } while (_sample2[0] == _sample1[0] && _sample2[1] == _sample1[1]);

        }

        //public void SetToEndState()
        //  Called if the user gives up or
        //  exhausts their guesses
        //  reveals all the samples on the map
        public void SetToEndState()
        {
            for (int r = 0; r < _rows; r++)
            {
                for (int c = 0; c < _cols; c++)
                {
                    if (r == _sample1[1] && c == _sample1[0])
                        _grid[r, c] = '$';

                    else if (r == _sample2[1] && c == _sample2[0])
                        _grid[r, c] = '$';
                }
            }
        }

        //public void SetToStartState()
        //accepts no input
        //returns no input
        //called when user clicks restart in the file menu dropdown
        //re initializes a ScanAnalyzer to its start state
        // -keeps sample locations
        // -returns _curGuess to zero
        // -removes all hints
        // -resets _found1 and _found2 to false
        public void SetToStartState()
        {
            _found1 = false;
            _found2 = false;
            _curGuesses = 0;
            PopulateArray();
        }

    }
}

```
