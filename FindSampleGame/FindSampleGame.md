```csharp
//David McGinn
//10 - 1 - 18
//CMPS-4143
//This program is a Find Sample Game. The player guesses
//co-ordinates and is given feedback on the location of samples
//the player may make a custom grid size > 1x1 and < 11x11
//to view instructions on how to play click Help > How to play

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace FindSampleGame
{
    public partial class FindSampleGame : Form
    {
        private ScanAnalyzer _scan;
        private bool _turn = true;


        public FindSampleGame()
        {
            InitializeComponent();
        }

        //File > Exit is clicked
        private void exitToolStripMenuItem_Click(object sender, EventArgs e)
        {
            Application.Exit();
        }

        //Help > How to Play is clicked
        private void howToPlayToolStripMenuItem_Click(object sender, EventArgs e)
        {
            //show a message box with game instructions
            MessageBox.Show("Your objective is to find the two hidden samples" +
                " within the allowed number of guesses.\nSimply enter" +
                " a valid co ordinate and press the Make Guess button." +
                "\nYou will see an arrow pointing you toward the sample" +
                " if you guess incorrectly, or a $ if you guess correctly." +
                "\n\nTo setup a game, enter a number of columns and rows in" +
                " the 'Setup' section of the main window." +
                " Be sure your grid is larger than 1x1 and smaller than 11x11!" +
                " \nThen, enter the ammount of guesses you would like to be" +
                "able to make." +
                " You may have anywhere from 1 to 999 guesses" +
                "\n\nYou may restart at any time by selecting file > restart." +
                " You will not be able to restart if you have lost the game!",
                "How to Play");
        }

        //Help > About is clicked
        private void aboutToolStripMenuItem_Click(object sender, EventArgs e)
        {
            MessageBox.Show("A Find Sample game by David McGinn" +
                "\n\nCreated for CMPS-4143-101" +
                " To view instructions, click Help > How to Play" +
                "\n\nfor more information please email me at this" +
                " webzone: notarealaddress@geocities.co.jp", "About");
        }

        //File > Give Up is clicked
        private void giveUpToolStripMenuItem_Click(object sender, EventArgs e)
        {
            EndGame();
        }

        //Enable the correct items and display the grid
        private void SetupGame()
        {
            MakeGuess.Enabled = true;
            GuessCols.Enabled = true;
            GuessRows.Enabled = true;
            giveUpToolStripMenuItem.Enabled = true;
            GameWindow.Text = _scan.DisplayGrid();
            GuessesUsed.Text = "Guesses used: " + _scan.CurGuesses;
        }

        //EndGame should be triggered if give up is selected
        //  or if guesses expires
        private void EndGame()
        {
            MakeGuess.Enabled = false;
            giveUpToolStripMenuItem.Enabled = false;
            restartToolStripMenuItem.Enabled = false;
            _scan.SetToEndState();
            GameWindow.Text = _scan.DisplayGrid();
            //had to use the ? operator somewhere
            MessageBox.Show((_scan.GameOver()) ? "Out of Guesses" : "Given Up", "Game Over");

        }

        //once the NewGame button is clicked the game is immediately started
        private void NewGame_Click(object sender, EventArgs e)
        {
            int rows, cols, guesses;
            bool p;

            //ensure valid inputs for rows, cols, and guesses
            //1x1 is not a valid grid since 2 samples must be present
            p = int.TryParse(NewCols.Text, out cols);
            if (p && cols <= 10 && cols >0)
            {
                p = int.TryParse(NewRows.Text, out rows);
                if (p && rows <= 10 && rows > 0)
                {
                    p = int.TryParse(NewGuess.Text, out guesses);
                    if (p && guesses > 0)
                    {
                        if (rows == cols && cols == 1)
                            MessageBox.Show("Grid cannot be 1x1", "Error");
                        else
                        {
                            _scan = new ScanAnalyzer(rows, cols, guesses);
                            SetupGame();
                        }
                    }
                    else
                        MessageBox.Show("Make Sure guesses is a valid" +
                            " positive interger", "rows invalid");
                }
                else
                    MessageBox.Show("Make Sure the Number of rows is" +
                        " less than 10 but greater than 0", "rows invalid");
            }
            else
                MessageBox.Show("Make sure the number of columns is" +
                    " less than 10 but greater than 0", "Guesses Invalid");
        }

        //MakeGuess is clicked
        //  should call ScanAnalyzer object's EvaluateGuess method
        //  wanted to try some exception handling here
        private void MakeGuess_Click(object sender, EventArgs e)
        {
            bool p, correct;
            int xcord;
            int ycord;

            p = int.TryParse(GuessCols.Text, out xcord);
            if(p)
            {
                p = int.TryParse(GuessRows.Text, out ycord);
                if(p)
                {
                    //make sure guess is within range
                    try
                    {
                        correct = _scan.EvaluateGuess(xcord, ycord, _turn);
                        _turn = !_turn;
                        GuessesUsed.Text = "Guesses Used: " + _scan.CurGuesses;
                        GameWindow.Text = _scan.DisplayGrid();
                        if(_scan.GameWon())
                        {
                            WinGame();
                        }
                        else if(_scan.GameOver())
                        {
                            EndGame();
                        }
                    }
                    catch(IndexOutOfRangeException)
                    {
                        MessageBox.Show("Guess is out of bounds", "error");
                    }
                }
            }
        }

        //restart is clicked
        //user may restart as long as the game isn't lost
        private void restartToolStripMenuItem_Click(object sender, EventArgs e)
        {
            _scan.SetToStartState();
            GameWindow.Text = _scan.DisplayGrid();
            GuessesUsed.Text = "Guesses Used: " + _scan.CurGuesses;
        }

        //called when game is won
        private void WinGame()
        {
            MessageBox.Show("You Win", "Congratulations");
            MakeGuess.Enabled = false;
            giveUpToolStripMenuItem.Enabled = false;
        }
    }
}

```
