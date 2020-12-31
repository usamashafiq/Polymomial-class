#include <iostream>
using namespace std;
class Polynomial
{
	//define private member functions
private:
	int coef[100];  // array of coefficients
					// coef[0] would hold all coefficients of x^0
					// coef[1] would hold all x^1
					// coef[n] = x^n ...
	int deg;        // degree of polynomial (0 for the zero polynomial)
					//define public member functions
public:
	Polynomial::Polynomial() //default constructor
	{
		for (int i = 0; i < 100; i++)
		{
			coef[i] = 0;
		}
	}
	void set(int a, int b) //setter function
	{
		//coef = new Polynomial[b+1];
		coef[b] = a;
		deg = degree();
	}
	int degree()
	{
		int d = 0;
		for (int i = 0; i < 100; i++)
			if (coef[i] != 0) d = i;
		return d;
	}
	void print()
	{
		for (int i = 99; i >= 0; i--) {
			if (coef[i] != 0) {
				cout << coef[i] << "x^" << i << " ";
			}
		}
	}
	// use Horner's method to compute and return the polynomial evaluated at x
	int evaluate(int x)
	{
		int p = 0;
		for (int i = deg; i >= 0; i--)
			p = coef[i] + (x * p);
		return p;
	}
	// differentiate this polynomial and return it
	Polynomial differentiate()
	{
		if (deg == 0) {
			Polynomial t;
			t.set(0, 0);
			return t;
		}
		Polynomial deriv;// = new Polynomial ( 0, deg - 1 );
		deriv.deg = deg - 1;
		for (int i = 0; i < deg; i++)
			deriv.coef[i] = (i + 1) * coef[i + 1];
		return deriv;
	}
	Polynomial plus(Polynomial b)
	{
		Polynomial a = *this; //a is the poly on the L.H.S
		Polynomial c;
		for (int i = 0; i <= a.deg; i++) c.coef[i] += a.coef[i];
		for (int i = 0; i <= b.deg; i++) c.coef[i] += b.coef[i];
		c.deg = c.degree();
		return c;
	}
	Polynomial minus(Polynomial b)
	{
		Polynomial a = *this; //a is the poly on the L.H.S
		Polynomial c;
		for (int i = 0; i <= a.deg; i++) c.coef[i] += a.coef[i];
		for (int i = 0; i <= b.deg; i++) c.coef[i] -= b.coef[i];
		c.deg = c.degree();
		return c;
	}
	Polynomial times(Polynomial b)
	{
		Polynomial a = *this; //a is the poly on the L.H.S
		Polynomial c;
		for (int i = 0; i <= a.deg; i++)
			for (int j = 0; j <= b.deg; j++)
				c.coef[i + j] += (a.coef[i] * b.coef[j]);
		c.deg = c.degree();
		return c;
	}
};
int main()
{
	Polynomial a, b, c, d;
	a.set(7, 4); //7x^4
	a.set(1, 2); //x^2
	b.set(6, 3); //6x^3
	b.set(-3, 2); //-3x^2
	c = a.minus(b); // (7x^4 + x^2) - (6x^3 - 3x^2)
	c.print();
	cout << "\n";
	c = a.times(b); // (7x^4 + x^2) * (6x^3 - 3x^2)
	c.print();
	cout << "\n";
	d = c.differentiate().differentiate();
	d.print();

	cout << "\n";

	cout << c.evaluate(2); //substitue x with 2
	cin.get();
}


Corban footprint
#include <iostream>
#include <vector>
using namespace std;

class CarbonFootPrint
{
	//class declarations
public:
	virtual double getCarbonFootPrint();
};

//class implementation
double CarbonFootPrint::getCarbonFootPrint()
{
	return 0;
}

class Building : CarbonFootPrint
{
	//class declarations
public:
	Building(double e = 0, int m = 12); //constructor
	~Building(); //destructor
	double setElectric();
	virtual double getCarbonFootPrint();

private:
	double electric;
	int months;
};

//class implementation
Building::Building(double e, int m)
{
	electric = e;
	months = m;
}

Building::~Building()
{

}

double Building::setElectric()
{
	cout << "Enter your monthly electric in KWH: " << endl;
	cin >> electric;
	return electric;
}

double Building::getCarbonFootPrint()
{
	//I would like to print out the variable information for each object created
	//and then 
	cout << "The carbon footprint for this house is " << endl;
	//when it iterates through the vector.
	return(electric * months);
}


class Car : CarbonFootPrint
{
public:
	Car(double = 0, double = 0); //constructor
	~Car(); //destructor
	double setYearlyMiles();
	double setAverageMPG();
	virtual double getCarbonFootPrint();

private:
	double yearlyMiles, averageMPG;
	int co2 = 9;
};

//class implementation
Car::Car(double ym, double mpg)
{
	yearlyMiles = ym;
	averageMPG = mpg;
}

Car::~Car()
{

}

double Car::setYearlyMiles()
{
	cout << "Enter in your yearly miles: " << endl;
	cin >> yearlyMiles;
	return yearlyMiles;
}

double Car::setAverageMPG()
{
	cout << "Enter in your average miles per gallon: " << endl;
	cin >> averageMPG;
	return averageMPG;
}

double Car::getCarbonFootPrint()
{
	//I would like to print out the variable information for each object created
	//and then 
	cout << "The carbon footprint for this car is " << endl;
	//when it iterates through the vector.
	return((yearlyMiles * averageMPG) * co2);
}

class Bicycle : CarbonFootPrint
{
public:
	Bicycle(double = 0, int = 34); //constructor
	~Bicycle(); //destructor
	double setMiles();
	virtual double getCarbonFootPrint();

private:
	int calories;
	double miles;
};

//class implementation
Bicycle::Bicycle(double m, int c)
{
	miles = m;
	calories = c;
}

Bicycle::~Bicycle()
{

}

double Bicycle::setMiles()
{
	cout << "Enter in number of miles: " << endl;
	cin >> miles;
	return miles;
}

double Bicycle::getCarbonFootPrint()
{
	//I would like to print out the variable information for each object created
	//and then 
	cout << "The carbon footprint for this bicycle is " << endl;
	//when it iterates through the vector.
	return (miles * calories);
}
int main()
{
	vector <CarbonFootPrint> *list;
	int answer, i;

	cout << "Welcome to the Carbon Footprint Calculator!\n" << endl;

	do
	{
		cout << "Main Menu\n" << endl;
		cout << "1: Set house info.\n" << endl;
		cout << "2: Set car info.\n" << endl;
		cout << "3: Set bicycle info.\n" << endl;
		cout << "4: Get carbon footprint for all items set.\n" << endl;
		cin >> answer;

		switch (answer)
		{
		case 1:
		{
			cout << "\n" << endl;
			Building *anotherBuilding;
			anotherBuilding = new Building;
			anotherBuilding->setElectric();
			cout <<endl<< anotherBuilding->getCarbonFootPrint();
			cout << "\n" << endl;

			break;
		}

		case 2:
		{
			cout << "\n" << endl;
			Car *anotherCar;
			anotherCar = new Car;
			anotherCar->setYearlyMiles();
			anotherCar->setAverageMPG();
			cout << endl << anotherCar->getCarbonFootPrint();
			cout << "\n" << endl;

			break;
		}

		case 3:
		{
			cout << "\n" << endl;
			Bicycle *anotherbike;
			anotherbike = new Bicycle;
			anotherbike->setMiles();
			cout << endl << anotherbike->getCarbonFootPrint();
			cout << "\n" << endl;

			break;
		}

		case 4:
		{

			//have it iterate through the vector and print out each carbon footprint.
			break;
		}

		default:
		{
			cout << answer << " is not a valid option" << endl;

			break;
		}
		}
	} while (answer != 4);

	system("pause");
	return 0;
}
