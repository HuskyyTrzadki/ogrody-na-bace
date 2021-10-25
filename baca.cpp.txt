//JAKUB JOCHYMEK
#include <iostream>
//OWOCOWY OGRODEK grrrr
using namespace std;
class BRANCH_CLASS;
class FRUIT_CLASS {
private:
	BRANCH_CLASS* fromWchichBranch;
	unsigned int weight;
	unsigned int lengthWhereIsFruit;
	FRUIT_CLASS* next;
	FRUIT_CLASS* prev;
public:
	BRANCH_CLASS* getBranchPointer();
	FRUIT_CLASS* getNext();
	void displayAll();
	FRUIT_CLASS* getPrev();
	unsigned int getWeight();
	void setWeight(unsigned int);
	unsigned int getLength();
	void growthFruit();
	void fadeFruit();
	void pluckFruit();
	void setPrev(FRUIT_CLASS*);
	void setNext(FRUIT_CLASS*);
	void setParent(BRANCH_CLASS*);
	FRUIT_CLASS();
	~FRUIT_CLASS();
	FRUIT_CLASS(int, BRANCH_CLASS*, int);
	unsigned int getLengthWhereIsFruit();
	void setLengthWhereIsFruit(unsigned int);
	FRUIT_CLASS(const FRUIT_CLASS&);

};
class WOOD_CLASS;
class BRANCH_CLASS {
private:
	WOOD_CLASS* fromWchichWood;
	unsigned int FruitsTotal;
	unsigned int length;
	unsigned int heightThatItGrows;
	unsigned int totalWeight;
	FRUIT_CLASS* headOfFruits;
	BRANCH_CLASS* next;
	BRANCH_CLASS* prev;
public:
	BRANCH_CLASS(int, WOOD_CLASS*);
	~BRANCH_CLASS();
	BRANCH_CLASS(const BRANCH_CLASS&);
	FRUIT_CLASS* getFruitPointer(unsigned int);
	unsigned int getFruitsTotal();
	unsigned int getWeightsTotal();
	void setParent(WOOD_CLASS*);
	unsigned int getHeight();
	unsigned int getLength();
	FRUIT_CLASS* getFruitHead();
	BRANCH_CLASS* getBranchPointer(unsigned int);
	void growthBranch();
	void fadeBranch();
	void harvestBranch(unsigned int);
	void cutBranch(unsigned int);
	void displayAll();



	void setLength(unsigned int);
	void setHeight(unsigned int);
	void setWeightsTotal(unsigned int);
	void setFruitsTotal(unsigned int);
	WOOD_CLASS* getWoodPointer();
	BRANCH_CLASS* getNext();
	BRANCH_CLASS* getPrev();
	BRANCH_CLASS();
	void setPrev(BRANCH_CLASS*);
	void setNext(BRANCH_CLASS*);

};
class GARDEN_CLASS;
class WOOD_CLASS {
private:
	int nrOfBranches;
	unsigned int nrOfFruits;
	int totalWeight;
	unsigned int height;
	unsigned int number;

	GARDEN_CLASS* fromWchichGarden;//ustaw na nulla w mostruktore
	BRANCH_CLASS* headOfBranches;
	WOOD_CLASS* next;
	WOOD_CLASS* prev;

public:
	WOOD_CLASS();
	
	WOOD_CLASS(int, GARDEN_CLASS*);
	~WOOD_CLASS();
	void setParent(GARDEN_CLASS* x);
	unsigned int getBranchesTotal();
	void setBranchesTotal(unsigned int);
	unsigned int getWeightsTotal();
	void setWeightsTotal(unsigned int);
	unsigned int getFruitsTotal();
	void setFruitsTotal(unsigned int);
	unsigned int getNumber();
	void displayAll();
	WOOD_CLASS(const WOOD_CLASS&);
	void setNumber(unsigned int);
	unsigned int getHeight();
	void setHeight(unsigned int);
	unsigned int getWeight();
	void growthWood();
	void fadeWood();
	void harvestWood(unsigned int);
	void cutWood(unsigned int);
	void cloneBranch(BRANCH_CLASS*);
	GARDEN_CLASS* getGardenPointer();
	BRANCH_CLASS* getBranchPointer(unsigned int);

	WOOD_CLASS* getNext();
	WOOD_CLASS* getPrev();
	void setPrev(WOOD_CLASS*);
	void setNext(WOOD_CLASS*);

};

class GARDEN_CLASS {
private:
	unsigned int counter;
	unsigned int nrOfTrees;
	unsigned int nrOfBranches;
	unsigned int nrOfFruits;
	unsigned int totalWeight;
	WOOD_CLASS* headOfTrees;


public:
	GARDEN_CLASS();
	~GARDEN_CLASS();
	unsigned int getWoodsTotal();
	void setWoodsTotal(unsigned int);
	unsigned int getBranchesTotal();
	void setBranchesTotal(unsigned int);
	unsigned int getFruitsTotal();
	void displayAll();

	void setFruitsTotal(unsigned int);
	int	getWeightsTotal();
	unsigned int getCounter();
	WOOD_CLASS* getWoodPointer(unsigned int);
	void setCounter(unsigned int);
	void setWeightTotal(int);
	void plantWood();
	void extractWood(unsigned int);
	void growthGarden();
	void fadeGarden();
	void harvestGarden(unsigned int a_weight);
	void cloneWood(unsigned int );
	WOOD_CLASS* getHeadOfTrees();
};





//FRUIT///////////////////////////////////
FRUIT_CLASS::FRUIT_CLASS(int WEIGHT, BRANCH_CLASS* BRANCH, int lengthWhereIsFruit) {
	weight = WEIGHT;
	fromWchichBranch = BRANCH;
	this->lengthWhereIsFruit = lengthWhereIsFruit;
	prev = next = this;
}
FRUIT_CLASS::FRUIT_CLASS() {
	weight = lengthWhereIsFruit = 0;
	fromWchichBranch = NULL;
	prev = next = this;

}
FRUIT_CLASS::~FRUIT_CLASS() {
	this->pluckFruit();

}
FRUIT_CLASS::FRUIT_CLASS(const FRUIT_CLASS& toCopy)
{
	this->lengthWhereIsFruit = 0;
	this->fromWchichBranch = NULL;
	this->setNext(this);
	this->setPrev(this);
	this->weight = toCopy.weight;
}
unsigned int FRUIT_CLASS::getLength() { //pozycja owoca
	return lengthWhereIsFruit;
}
unsigned int FRUIT_CLASS::getWeight() {
	return weight;
}
void FRUIT_CLASS::setParent(BRANCH_CLASS* x) {
	this->fromWchichBranch = x;

}
FRUIT_CLASS* FRUIT_CLASS::getNext() {
	return next;
}
FRUIT_CLASS* FRUIT_CLASS::getPrev() {
	return prev;
}
void FRUIT_CLASS::setNext(FRUIT_CLASS* x) {
	next = x;

}
void FRUIT_CLASS::setPrev(FRUIT_CLASS* x) {
	prev = x;

}
void FRUIT_CLASS::setWeight(unsigned int x) {
	weight = x;
}


void FRUIT_CLASS::growthFruit() {
	weight++;
	if(fromWchichBranch!=NULL){
		fromWchichBranch->setWeightsTotal(fromWchichBranch->getWeightsTotal() + 1);
		if (fromWchichBranch->getWoodPointer() != NULL) {
			fromWchichBranch->getWoodPointer()->setWeightsTotal(fromWchichBranch->getWoodPointer()->getWeightsTotal() + 1);
			if (fromWchichBranch->getWoodPointer()->getGardenPointer() != NULL) {
				fromWchichBranch->getWoodPointer()->getGardenPointer()->setWeightTotal(fromWchichBranch->getWoodPointer()->getGardenPointer()->getWeightsTotal() + 1);
			}
		}
	}
		
	
}
void FRUIT_CLASS::fadeFruit() {
	if (weight > 0) {
		weight--;
		if (fromWchichBranch != NULL && fromWchichBranch->getWeightsTotal() > 0) {
			fromWchichBranch->setWeightsTotal(fromWchichBranch->getWeightsTotal() - 1);
			if (fromWchichBranch->getWoodPointer() != NULL && fromWchichBranch->getWoodPointer()->getWeightsTotal() > 0) {
				fromWchichBranch->getWoodPointer()->setWeightsTotal(fromWchichBranch->getWoodPointer()->getWeightsTotal() - 1);
				if (fromWchichBranch->getWoodPointer()->getGardenPointer() != NULL && fromWchichBranch->getWoodPointer()->getGardenPointer()->getWeightsTotal() > 0) {
					fromWchichBranch->getWoodPointer()->getGardenPointer()->setWeightTotal(fromWchichBranch->getWoodPointer()->getGardenPointer()->getWeightsTotal() - 1);
				}
			}
		}
	}
	
	
	

}
void FRUIT_CLASS::pluckFruit() {
	if (weight > 0) {
		int x = getWeight();
		
		if (fromWchichBranch != NULL && fromWchichBranch->getWeightsTotal() >= x) {
			fromWchichBranch->setWeightsTotal(fromWchichBranch->getWeightsTotal() - x);
			if (fromWchichBranch->getWoodPointer() != NULL && fromWchichBranch->getWoodPointer()->getWeightsTotal() >= x) {
				fromWchichBranch->getWoodPointer()->setWeightsTotal(fromWchichBranch->getWoodPointer()->getWeightsTotal() - x);
				if (fromWchichBranch->getWoodPointer()->getGardenPointer() != NULL && fromWchichBranch->getWoodPointer()->getGardenPointer()->getWeightsTotal() >= x) {
					fromWchichBranch->getWoodPointer()->getGardenPointer()->setWeightTotal(fromWchichBranch->getWoodPointer()->getGardenPointer()->getWeightsTotal() - x);
				}
			}
		}
		setWeight(0);
	}
	
	
	
	

}

unsigned int FRUIT_CLASS::getLengthWhereIsFruit() {
	return lengthWhereIsFruit;
}
void FRUIT_CLASS::setLengthWhereIsFruit(unsigned int x) {
	lengthWhereIsFruit = x;
}

BRANCH_CLASS* FRUIT_CLASS::getBranchPointer() {
	return fromWchichBranch;
}




//BRANCH/////////////////////////////////////////////////////////////////
BRANCH_CLASS::BRANCH_CLASS(int HeightThatItGrows, WOOD_CLASS* FromWchichWood) {
	FruitsTotal = 0;
	length = 0;
	this->fromWchichWood = FromWchichWood;
	heightThatItGrows = HeightThatItGrows;
	headOfFruits = new FRUIT_CLASS(0, this, 0); // pierwsze to waga, drugie to rodzic, trzecie to index
	totalWeight = 0;
	FruitsTotal = 0;
	prev = next = this;



}
BRANCH_CLASS::~BRANCH_CLASS() {
	FRUIT_CLASS* head = headOfFruits;
	//pojebao mnie i ide od konca
	FRUIT_CLASS* helper = head->getPrev();
	cutBranch(0);

	
	if (getWoodPointer() != NULL && getWoodPointer()->getWeightsTotal() >= 0) {
		(this->getWoodPointer())->setBranchesTotal((this->getWoodPointer()->getBranchesTotal()) - 1);
		if (getWoodPointer()->getGardenPointer() != NULL && getWoodPointer()->getGardenPointer()->getWeightsTotal() >= 0) {
			getWoodPointer()->getGardenPointer()->getBranchesTotal() - 1;
		}
	}

	
	delete headOfFruits;
}
BRANCH_CLASS::BRANCH_CLASS(const BRANCH_CLASS& from)
{
	this->FruitsTotal = from.FruitsTotal;
	this->totalWeight = from.totalWeight;
	this->length = from.length;
	this->headOfFruits = new FRUIT_CLASS(0, NULL, -1);
	headOfFruits->setNext(headOfFruits);
	headOfFruits->setPrev(headOfFruits);
	FRUIT_CLASS* headFrom = from.headOfFruits;
	FRUIT_CLASS* helperFrom = headFrom->getNext();
	FRUIT_CLASS* headTo = this->headOfFruits;
	FRUIT_CLASS* helperTo = headTo->getNext();
	while (helperFrom != headFrom) {
		FRUIT_CLASS* nowyOwoc = new FRUIT_CLASS(*helperFrom);
		nowyOwoc->setLengthWhereIsFruit(helperFrom->getLengthWhereIsFruit());
		nowyOwoc->setParent(this);
		helperTo->setNext(nowyOwoc);
		headTo->setPrev(nowyOwoc);
		nowyOwoc->setPrev(helperTo);
		nowyOwoc->setNext(headTo);
		helperTo = helperTo->getNext();
		helperFrom = helperFrom->getNext();
	}
}
BRANCH_CLASS::BRANCH_CLASS() {
	fromWchichWood = NULL;
	FruitsTotal = 0;
	length = 0;
	heightThatItGrows = 0;
	prev = next = this;
	headOfFruits = new FRUIT_CLASS(0, this, 0); // pierwsze to waga, drugie to rodzic, trzecie to index
	FruitsTotal++;
	headOfFruits->setNext(headOfFruits);
	headOfFruits->setPrev(headOfFruits);
	totalWeight = 0;
	FruitsTotal = 0;
}
void setParent(BRANCH_CLASS*);
unsigned int BRANCH_CLASS::getWeightsTotal() { return totalWeight; }
void  BRANCH_CLASS::setWeightsTotal(unsigned int x) { totalWeight = x; }
unsigned int BRANCH_CLASS::getFruitsTotal() { return FruitsTotal; }
void  BRANCH_CLASS::setFruitsTotal(unsigned int x) { FruitsTotal = x; }
unsigned int BRANCH_CLASS::getHeight() { return heightThatItGrows; }
void  BRANCH_CLASS::setHeight(unsigned int x) { heightThatItGrows = x; }
unsigned int BRANCH_CLASS::getLength() { return length; }
void BRANCH_CLASS::setLength(unsigned int x) { length = x; }
void BRANCH_CLASS::displayAll() {
	std::cout << "-----fruit_count:" << getFruitsTotal() << " ";
	std::cout << "weights:" << getWeightsTotal() << std::endl;
	int max = getFruitsTotal(), i = 2;
	if (max > 0) std::cout << "-----fruits: \n";

	while (i <= 2 * max) {
		FRUIT_CLASS* fruit = getFruitPointer(i);
		if (fruit != NULL) {
			std::cout << "       *fruit at " << i << std::endl;
			std::cout << "       *length: " << fruit->getLength() << " weight: " << fruit->getWeight() << std::endl;
		}
		i += 2;
	}
}
void BRANCH_CLASS::growthBranch() {
	//dodanie dlugsoci galezi
	FRUIT_CLASS* head = headOfFruits;

	FRUIT_CLASS* helper = head->getNext();
	//dodanie do kazdego owoca po 1 wagi
	while (helper != head) {
		helper->growthFruit();
		helper = helper->getNext();
	}
	length++;
	if (getLength() % 2 == 0) {
		//trzeba dodac owoc na koniec
		this->FruitsTotal += 1;
		if (this->getWoodPointer() != NULL) {
			(this->getWoodPointer()->setFruitsTotal(this->getWoodPointer()->getFruitsTotal() + 1));
			if (this->getWoodPointer()->getGardenPointer() != NULL) {
				this->getWoodPointer()->getGardenPointer()->setFruitsTotal(getWoodPointer()->getGardenPointer()->getFruitsTotal() + 1);
			}

		}
		
		FRUIT_CLASS* temp = head->getPrev();
		int tempPosition = (head->getPrev())->getLengthWhereIsFruit();
		//w kostruktuorze kolejno: waga, rodzic galaz, dlugosc
		FRUIT_CLASS* newFruit = new FRUIT_CLASS(0, this, tempPosition + 2);
		//przepinanie,dodawanie
		newFruit->setNext(head);
		head->setPrev(newFruit);
		newFruit->setPrev(temp);
		temp->setNext(newFruit);

	}
}
void BRANCH_CLASS::fadeBranch() {

	if (length != 0) {
		length--;
		FRUIT_CLASS* head = headOfFruits;
		FRUIT_CLASS* helper = head->getNext();
		if (length > 0) {
			while (helper != head) {
				if (helper->getLengthWhereIsFruit() > length) {

					cutBranch(length);
					break;
				}
				else {
					helper->fadeFruit();
					helper = helper->getNext();
				}

			}

		}
	}

}

void BRANCH_CLASS::harvestBranch(unsigned int x) {
	FRUIT_CLASS* head = headOfFruits;
	FRUIT_CLASS* helper = head->getNext();
	while (helper != head) {
		if (x <= helper->getWeight()) {
			helper->pluckFruit();
		}
		helper = helper->getNext();
	}
}
void BRANCH_CLASS::cutBranch(unsigned int len) {
	FRUIT_CLASS* head = headOfFruits;
	FRUIT_CLASS* helper = head->getPrev();
	length = len;
	int howManyFruits = 0;
	while (helper != head && len < helper->getLengthWhereIsFruit()) {
		helper = helper->getPrev();
		FRUIT_CLASS* toDelete = helper->getNext();
		howManyFruits++;
		helper->setNext(head);
		head->setPrev(helper);
		delete toDelete;
	}
	if (FruitsTotal >= howManyFruits) {
		FruitsTotal -= howManyFruits;
	}
	
	if ((getWoodPointer() != NULL) && getWoodPointer()->getFruitsTotal()>=howManyFruits) {
		getWoodPointer()->setFruitsTotal(getWoodPointer()->getFruitsTotal() - howManyFruits);//drewno
		if (this->getWoodPointer()->getGardenPointer() != NULL && getWoodPointer()->getGardenPointer()->getFruitsTotal() >= howManyFruits) {
			this->getWoodPointer()->getGardenPointer()->setFruitsTotal(getWoodPointer()->getGardenPointer()->getFruitsTotal() - howManyFruits);
		}

	}
	


}
WOOD_CLASS* BRANCH_CLASS::getWoodPointer() { return fromWchichWood; }
BRANCH_CLASS* BRANCH_CLASS::getNext() { return next; }
FRUIT_CLASS* BRANCH_CLASS::getFruitPointer(unsigned int S) {
	if (S == 0) {
		return NULL;
	}
	FRUIT_CLASS* head = headOfFruits;
	FRUIT_CLASS* helper = head->getNext();
	while (helper != head && helper->getLengthWhereIsFruit() <= S) {
		if (helper->getLengthWhereIsFruit() == S) {
			return helper;
		}
		helper = helper->getNext();
	}
	return NULL;

}
void BRANCH_CLASS::setParent(WOOD_CLASS* x) {
	fromWchichWood = x;
}
BRANCH_CLASS* BRANCH_CLASS::getPrev() { return prev; }
void BRANCH_CLASS::setPrev(BRANCH_CLASS* t_prev) { prev = t_prev; }
void BRANCH_CLASS::setNext(BRANCH_CLASS* t_next) { next = t_next; }
FRUIT_CLASS* BRANCH_CLASS::getFruitHead() { return headOfFruits; }
//WOOD////////////////////////////////////////////////////////////

WOOD_CLASS::WOOD_CLASS(int Number, GARDEN_CLASS* FromWchichGarden) {
	height = 0;
	prev = next = this;
	number = Number;
	headOfBranches = new BRANCH_CLASS(0, this);// pierwsze to waga, drugie to rodzic, trzecie to index
	nrOfFruits = 0;
	nrOfBranches = 0;
	fromWchichGarden = FromWchichGarden;
	totalWeight = 0;
}


WOOD_CLASS::WOOD_CLASS(const WOOD_CLASS& from)
{
	this->nrOfFruits = from.nrOfFruits;
	this->nrOfBranches = from.nrOfBranches;
	this->totalWeight = from.totalWeight;
	this->height = from.height;
	this->number = number;
	this->fromWchichGarden = from.fromWchichGarden;
	this->headOfBranches = new BRANCH_CLASS(0,this);
	headOfBranches->setNext(headOfBranches);
	headOfBranches->setPrev(headOfBranches);
	BRANCH_CLASS* headFrom = from.headOfBranches;
	BRANCH_CLASS* helperFrom = headFrom->getNext();
	BRANCH_CLASS* headTo = this->headOfBranches;
	BRANCH_CLASS* helperTo = headTo->getNext();
	while (helperFrom != headFrom) {
		BRANCH_CLASS* nowaGalaz = new BRANCH_CLASS(*helperFrom);
		nowaGalaz->setLength(helperFrom->getLength());
		nowaGalaz->setParent(this);
		helperTo->setNext(nowaGalaz);
		headTo->setPrev(nowaGalaz);
		nowaGalaz->setPrev(helperTo);
		nowaGalaz->setNext(headTo);
		helperTo = helperTo->getNext();
		helperFrom = helperFrom->getNext();
	}
}
WOOD_CLASS::WOOD_CLASS() {
	height = 0;
	fromWchichGarden = NULL;
	totalWeight = 0;
	headOfBranches = new BRANCH_CLASS(0, this);// pierwsze to waga, drugie to rodzic, trzecie to index
	prev = next = this;
	nrOfFruits = 0;
	number = 0;
	nrOfBranches = 0;
}
void WOOD_CLASS::displayAll() {
	std::cout << ">>fruit_count:" << getFruitsTotal() << " ";
	std::cout << "branch_count:" << getBranchesTotal() << " ";
	std::cout << "weights:" << getWeightsTotal() << std::endl;
	int max = getBranchesTotal(), i = 3;
	if (max > 0) std::cout << ">>branches: \n";
	while (i <= 3 * max) {
		BRANCH_CLASS* branch = getBranchPointer(i);
		if (branch != NULL) {
			std::cout << "-----branch at " << i << std::endl;
			branch->displayAll();
		}
		i += 3;
	}
}

WOOD_CLASS::~WOOD_CLASS() {
	nrOfBranches = nrOfFruits = totalWeight = height = 0;
	cutWood(0);
	if (this->fromWchichGarden != NULL && this->fromWchichGarden->getWoodsTotal() > 0) {
		this->fromWchichGarden->setWoodsTotal(this->fromWchichGarden->getWoodsTotal() - 1);
	}
	delete this->headOfBranches;
}

BRANCH_CLASS* WOOD_CLASS::getBranchPointer(unsigned int x) {
	BRANCH_CLASS* head = headOfBranches;
	if (x <= 0) {
		return NULL;
	}
	BRANCH_CLASS* helper = head->getNext();
	while (helper != head && helper->getHeight() != x) {
		helper = helper->getNext();
	}
	if (helper->getHeight() == x) {
		return helper;
	}
	else {
		return NULL;
	}

}
void WOOD_CLASS::setParent(GARDEN_CLASS* x) {
	fromWchichGarden = x;
}
unsigned int WOOD_CLASS::getWeight() {
	return totalWeight;
}
unsigned int WOOD_CLASS::getHeight() { return height; }
void WOOD_CLASS::setHeight(unsigned int x) { height = x; }
unsigned int WOOD_CLASS::getBranchesTotal() { return nrOfBranches; }

void WOOD_CLASS::setBranchesTotal(unsigned int x) { nrOfBranches = x; }
unsigned int WOOD_CLASS::getWeightsTotal() { return totalWeight; }
unsigned int WOOD_CLASS::getNumber() { return number; }
void WOOD_CLASS::setWeightsTotal(unsigned int x) {
	totalWeight = x;

}
void WOOD_CLASS::setNumber(unsigned int Number) { number = Number; }
//unsigned int WOOD_CLASS::getHeight() {  }
void WOOD_CLASS::growthWood() {
	//dodanie dlugsoci galezi
	height = 1 + height;
	BRANCH_CLASS* head = headOfBranches;

	BRANCH_CLASS* helper = head->getNext();
	//dodanie do kazdego owoca po 1 wagi
	while (helper != head) {
		helper->growthBranch();
		helper = helper->getNext();
	}
	if (getHeight() % 3 == 0) {
		//trzeba dodac galaz na koniec
		this->nrOfBranches += 1; // w tym drzewie
		if (this->getGardenPointer() != NULL) {
			this->getGardenPointer()->setBranchesTotal(this->getGardenPointer()->getBranchesTotal() + 1);
		}
		//zapisuje ostatni element do  zeby go nie stracic
		BRANCH_CLASS* temp = head->getPrev();
		unsigned int tempPosition = (head->getPrev())->getHeight();
		BRANCH_CLASS* newBranch = new BRANCH_CLASS(tempPosition + 3, this);
		//nie ustawiasz preva sprawdz wyzej
		newBranch->setNext(head);
		newBranch->setPrev(temp);
		head->setPrev(newBranch);
		temp->setNext(newBranch);
	}
}
void WOOD_CLASS::fadeWood() {

	if (height > 0) {

		height--;
		BRANCH_CLASS* head = headOfBranches;
		BRANCH_CLASS* helper = head->getNext();
		while (helper != head) {
			if (helper->getHeight() > this->height) {

				helper->getNext()->setPrev(helper->getPrev());

				(helper->getPrev())->setNext(helper->getNext());
				delete helper;
				break;
			}
			else {
			
				helper->fadeBranch();
			
				helper = helper->getNext();
			}

		}


		//usuwanie kadego owoca powyzej zmniejszonej odleglosci

	}

}
void WOOD_CLASS::harvestWood(unsigned int x) {
	BRANCH_CLASS* head = headOfBranches;
	BRANCH_CLASS* helper = head->getNext();
	while (helper != head) {
		helper->harvestBranch(x);
		helper = helper->getNext();
	}
}

void WOOD_CLASS::cutWood(unsigned int x) {
	BRANCH_CLASS* head = headOfBranches;
	BRANCH_CLASS* helper = head->getPrev();
	height = x;

	while (helper != head && helper->getHeight() > x) {
		helper = helper->getPrev();
		BRANCH_CLASS* toDelete = helper->getNext();
	
		helper->setNext(head);
		head->setPrev(helper);
		delete toDelete;
	}

}
GARDEN_CLASS* WOOD_CLASS::getGardenPointer() { return fromWchichGarden; }
//BRANCH_CLASS* WOOD_CLASS::getBranchPointer(unsigned int x) {  }


WOOD_CLASS* WOOD_CLASS::getNext() { return next; }
WOOD_CLASS* WOOD_CLASS::getPrev() { return prev; }
unsigned int WOOD_CLASS::getFruitsTotal() { return nrOfFruits; }
void WOOD_CLASS::setFruitsTotal(unsigned int x) { nrOfFruits = x; }
void WOOD_CLASS::setPrev(WOOD_CLASS* t_prev) { prev = t_prev; }
void WOOD_CLASS::setNext(WOOD_CLASS* t_next) { next = t_next; }

void WOOD_CLASS::cloneBranch(BRANCH_CLASS* from) {
	BRANCH_CLASS* head = headOfBranches;
	BRANCH_CLASS* helper = head->getNext();//tu usuwamy normalnie idac do przodu
	while (helper != head && helper->getLength() != 0) {
		helper = helper->getNext();
	}
	if (helper->getLength() == 0) {
		BRANCH_CLASS* clone = new BRANCH_CLASS(*from);
		clone->setParent(this);
		clone->setNext(helper->getNext());
		clone->setPrev(helper->getPrev());
		helper->getNext()->setPrev(clone);
		helper->getPrev()->setNext(clone);
		totalWeight += from->getWeightsTotal();

		if (this->fromWchichGarden != NULL) {
			this->fromWchichGarden->setWeightTotal(this->fromWchichGarden->getWeightsTotal()+clone->getWeightsTotal());
			this->fromWchichGarden->setFruitsTotal(this->fromWchichGarden->getFruitsTotal() + clone->getFruitsTotal());
		}
		nrOfFruits += from->getFruitsTotal();
		clone->setHeight(helper->getHeight());
		delete helper;
		nrOfBranches++;
	}
}



//GARDEN/////////////////////////////////////////////////////////

GARDEN_CLASS::GARDEN_CLASS() {
	headOfTrees = new WOOD_CLASS(-1, this);
	nrOfBranches = nrOfFruits = nrOfTrees = counter = totalWeight = 0;
}
GARDEN_CLASS::~GARDEN_CLASS() {
	WOOD_CLASS* head = headOfTrees;
	WOOD_CLASS* helper = head->getPrev();
	while (helper != head) {
		WOOD_CLASS* toDelete = helper;
		helper = helper->getPrev();
		helper->setNext(toDelete->getNext());
		toDelete->getNext()->setPrev(helper);
		delete toDelete;
	}

}
unsigned int GARDEN_CLASS::getWoodsTotal() { return nrOfTrees; }
void GARDEN_CLASS::setWoodsTotal(unsigned int x) { nrOfTrees = x; }
unsigned int GARDEN_CLASS::getBranchesTotal() { return nrOfBranches; }
void GARDEN_CLASS::setBranchesTotal(unsigned int x) { nrOfBranches = x; }
unsigned int GARDEN_CLASS::getFruitsTotal() { return nrOfFruits; }
void GARDEN_CLASS::setFruitsTotal(unsigned int x) { nrOfFruits = x; }
int GARDEN_CLASS::getWeightsTotal() { return totalWeight; }
void GARDEN_CLASS::setWeightTotal(int x) { totalWeight = x; }
WOOD_CLASS* GARDEN_CLASS::getHeadOfTrees() { return headOfTrees; }
void GARDEN_CLASS::setCounter(unsigned int x) { counter = x; }
unsigned int GARDEN_CLASS::getCounter() { return counter; }
void GARDEN_CLASS::displayAll() {
	std::cout << "GARDEN:" << std::endl;
	std::cout << "fruit_count:" << getFruitsTotal() << " ";
	std::cout << "tree_count:" << getWoodsTotal() << " ";
	std::cout << "branch_count:" << getBranchesTotal() << " ";
	std::cout << "weights:" << getWeightsTotal() << std::endl;
	std::cout << "trees: \n";
	int max = getWoodsTotal(), i = 0;
	while (i <= max) {
		WOOD_CLASS* wood = getWoodPointer(i);

		if (i != nrOfTrees + 1 && wood != NULL) {
			std::cout << "tree nr " << i << std::endl;
			wood->displayAll();
			std::cout << std::endl;
		}
		i++;
	}
	std::cout << std::endl;
	std::cout << "/ / / / / / / /";
	std::cout << std::endl << std::endl;
}
void GARDEN_CLASS::plantWood() {
	WOOD_CLASS* head = headOfTrees;

	if (counter == 0) {
		WOOD_CLASS* helper = head->getPrev();
		WOOD_CLASS* newBranch = new WOOD_CLASS(helper->getNumber() + 1, helper->getGardenPointer());
		newBranch->setNext(head);
		newBranch->setPrev(helper);
		head->setPrev(newBranch);
		helper->setNext(newBranch);

	}
	else {
		WOOD_CLASS* helper = head->getNext();
		int w = -1;
		while (helper != head) {
			w++;
			if (helper->getNumber() == w) {// od 0
				helper = helper->getNext();
			}
			else {
				WOOD_CLASS* nowy = new WOOD_CLASS(w, helper->getGardenPointer());
				nowy->setPrev(helper->getPrev());
				nowy->setNext(helper);
				helper->getPrev()->setNext(nowy);
				helper->setPrev(nowy);
				break;

			}
		}
		if (counter > 0) {
			counter--;
		}

	}
	nrOfTrees++;
};
void GARDEN_CLASS::extractWood(unsigned int x) {
	WOOD_CLASS* head = headOfTrees;

	if (x < nrOfTrees / 2) {
		WOOD_CLASS* helper = head->getNext();
		while (helper != head) {
			if (helper->getNumber() == x) {
				
				if (helper != head->getPrev()) {
					counter++;
				}
				helper->getNext()->setPrev(helper->getPrev());
				(helper->getPrev())->setNext(helper->getNext());

				delete helper;

				break;


			}
			else {
				helper = helper->getNext();
			}
		}

	}
	else {
		WOOD_CLASS* helper = head->getPrev();
		while (helper != head) {
			if (helper->getNumber() == x) {
				if (helper != head->getPrev()) {
					counter++;
				}
				helper->getNext()->setPrev(helper->getPrev());
				(helper->getPrev())->setNext(helper->getNext());

				delete helper;

				break;


			}
			else {
				helper = helper->getPrev();
			}
		}


	}


};
void GARDEN_CLASS::growthGarden() {
	//dodanie dlugsoci galezi
	WOOD_CLASS* head = headOfTrees;
	WOOD_CLASS* helper = head->getNext();
	//dodanie do kazdego owoca po 1 wagi
	while (helper != head) {
		helper->growthWood();
		helper = helper->getNext();
	}
};
WOOD_CLASS* GARDEN_CLASS::getWoodPointer(unsigned int x) {
	WOOD_CLASS* head = headOfTrees;

	WOOD_CLASS* helper = head->getNext();
	while (helper != head && helper->getNumber() != x) {
		helper = helper->getNext();
	}
	if (helper->getNumber() == x) {
		return helper;
	}
	else {
		return NULL;
	}

}
void GARDEN_CLASS::fadeGarden() {
	//dodanie dlugsoci galezi
	WOOD_CLASS* head = headOfTrees;
	WOOD_CLASS* helper = head->getNext();
	while (helper != head) {
		helper->fadeWood();
		helper = helper->getNext();
	}
};
void GARDEN_CLASS::harvestGarden(unsigned int x) {
	WOOD_CLASS* head = headOfTrees;
	WOOD_CLASS* helper = head->getNext();
	while (helper != head) {
		helper->harvestWood(x);
		helper = helper->getNext();
	}
};
void GARDEN_CLASS::cloneWood(unsigned int num) {
	//nowe drzewko o najniszym mozliwym numerze
	WOOD_CLASS* clone = getWoodPointer(num);
	WOOD_CLASS* head = headOfTrees;
	if (counter == 0) {
		//na koniec
		WOOD_CLASS* helper = head->getPrev();
		WOOD_CLASS* newWood = new WOOD_CLASS(*clone);
		nrOfFruits += clone->getFruitsTotal();
		totalWeight += clone->getWeightsTotal();
		nrOfBranches += clone->getBranchesTotal();
		newWood->setNext(head);
		newWood->setPrev(helper);
		head->setPrev(newWood);
		helper->setNext(newWood);

	}
	else {
		WOOD_CLASS* helper = head->getNext();
		int w = -1;
		while (helper != head) {
			w++;
			if (helper->getNumber() == w) {// od 0
				helper = helper->getNext();
			}
			else {
				WOOD_CLASS* newWood = new WOOD_CLASS(*clone);
				
				newWood->setPrev(helper->getPrev());
				newWood->setNext(helper);
				helper->getPrev()->setNext(newWood);
				helper->setPrev(newWood);
				nrOfFruits += clone->getFruitsTotal();
				totalWeight += clone->getWeightsTotal();
				nrOfBranches += clone->getBranchesTotal();
				break;

			}
		}
		if (counter > 0) {
			counter--;
		}

	}
	nrOfTrees++;
};