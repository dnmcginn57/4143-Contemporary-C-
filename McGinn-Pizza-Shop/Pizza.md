```csharp
//David McGinn
//11-7-18
//CMPS4143
//This is a pizza class.
//It keeps track of it's own name, size, toppings, and price


using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Collections;

namespace McGinn_Pizza_Shop
{
    public class Pizza
    {
        private string _name, _size, _crust;
        private ArrayList _toppings;
        private double _price;

        public double Price
        {
            get { return _price; }
        }

        //sets name and size right off the bat
        public Pizza(string name, string size)
        {
            _name = name;
            _size = size;
            _crust = " ";
            _toppings = new ArrayList();
            CalculatePrice();
        }

        //overloaded constructor for when crust is specified
        public Pizza(string name, string size, string crust)
        {
            _name = name;
            _size = size;
            _crust = crust;
            _toppings = new ArrayList();
            CalculatePrice();
        }

        //gives a modular output that can be added to invoice
        public override string ToString()
        {
            string s = "";



            s += _name + " - " + _crust + " - " + _size + "..........." + _price;


            s += Environment.NewLine;

            foreach(string t in _toppings)
            {
                s += "  " + t;
                s += Environment.NewLine;
            }

            return s;
        }

        //some how, some way populates the array of toppings
        public void AddToppings(ArrayList tops)
        {

            _toppings.AddRange(tops);
            CalculatePrice();
        }

        //calculates price based on size and ammount of toppings
        private void CalculatePrice()
        {
            //set the price based on size.
            switch (_size)
            {
                case ("Fetta"):
                    _price = 1.00;
                    break;
                case ("Personale"):
                    _price = 3.50;
                    break;
                case ("Piccolo"):
                    _price = 5.00;
                    break;
                case ("Medio"):
                    _price = 7.50;
                    break;
                case ("Grande"):
                    _price = 15.00;
                    break;
            }
            //add toppings to the price
            _price = _price + (_toppings.Count * .5);

        }


    }
}

```
