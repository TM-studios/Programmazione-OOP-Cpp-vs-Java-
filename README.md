# C++ - Object Oriented Programming (OOP)
Questa documentazione ha lo scopo di comparare la programmazione ad oggetti in C++ con quella in Java.

Scritta da [@TheiPhoneDev](https://github.com/TheiPhoneDev)

iniziamo dalle basi:

## Struttura di una classe in C++
```cpp
class nome_classe {
	//dichiarazione attributi e metodi
}
```
### Dichiarazione di attributi e metodi in una classe
```cpp
class nome_classe {
	private:
		int n1;
		string nome;
		char character;
		bool value;
	public:
		void metodo1(){}
		int metodo(){}
		int getN1(){}
		int setN2(){}
		
}
```
In base al tipo di visibilità che vogliamo dare agli attributi si usano le keyword: **private**,  **protected**, **public**.
- Gli attributi di tipo **private** possono essere visti solo dalla classe stessa e non da classi esterne e sottoclassi.
- Gli attributi di tipo **protected** sono una via di mezzo tra private e public, ossia sono private per le classi esterne, ma sono ereditabili dalle sottoclassi.
- Gli attributi di tipo **public** possono essere visti da chiunque.

Per i metodi il discorso cambia, perché sono sempre di tipo **public**, poiché sono il modo in cui l'interfaccia interagisce con la classe.

## Inizializzazione di una classe

Per inizializzare una classe in C++ usiamo un metodo costruttore, considerato come un metodo speciale, che ci permette di inizializzare tutti gli attributi della classe e prepararli così per l'utilizzo all'interno del programma. Ed è l'unico metodo ad essere chiamato con lo stesso nome della classe.
```cpp
class nome_classe {
	private:
		int n1;
		string nome;
		char character;
		bool value;
	public:
		nome_classe(){}
		void metodo1(){}
		
		
}
```
Il costruttore può anche non contenere alcun valore al suo interno, poiché quando richiamato inizializzare automaticamente gli attributi, altrimenti:

*esempio di costruttore inizializzato manualmente*
```cpp
class nome_classe {
	private:
		int n1;
		string nome;
		char character;
		bool value;
	public:
		nome_classe(){
			n1=0;
			nome="";
			character='';
			value=false;
		}
		void metodo1(){}
		
		
}
```
Da puntualizzare anche il fatto che il costruttore di default, nel caso in cui non stiamo utilizzando altri tipi di costruttore come ad esempio quello parametrizzato, può essere omesso del tutto, poiché il compilatore lo riconosce come mancante e lo andrà ad inserire lui.

### Uso di un costruttore parametrizzato

Nel caso in cui abbiamo necessità di utilizzare un costruttore parametrizzato, la dichiarazione è la seguente:
```cpp
class nome_classe {
	private:
		int n1;
		string nome;
		char character;
		bool value;
	public:
		nome_classe(){}
		nome_classe(int n1, string nome, char character, bool value) {
			this->n1=n1;
			this->nome=nome;
			this->character=character;
			this->value=value;
		}
		void metodo1(){}
}
```
In questo caso C++ richiede che il costruttore di default sia richiamato insieme a quello parametrizzato, altrimenti ci darà errore nella console. Questo perché richiede una pre-inizializzazione a valori di default, in modo tale da permetterci di usare successivamente il costruttore parametrizzato con dati che magari possono esserci passati tramite input.

Da notare che la keyword **this**, viene utilizzata per riferirsi all'attributo della classe in modo tale che il parametro che viene passato nel costruttore abbia lo stesso nome dell'attributo e così il compilatore capisce a chi ci stiamo riferendo. E' utile per non usare nomi di variabili diverse.

Il costruttore parametrizzato è utile per sfruttare il concetto di **Polimorfismo** che è uno dei tre concetti cardine dell'OOP, assieme **Incapsulamento** ed **Ereditarietà**. Il **polimorfismo** permette agli oggetti di assumere "forme" diverse in base al tipo di utilizzo che vogliamo farne.

## Dichiarazione di una sottoclasse
Una sottoclasse è una classe che eredità attributi e metodi di una super classe, o classe base, e introduce anche i suoi attributi e metodi.
```cpp
class Superclasse {
	protected:
		int anno;
		string nome;
	public:
		Superclasse(){}
		Superclasse(int anno, string nome) {
			this->anno=anno;
			this->nome=nome;
		}
		void metodo1(){}
}

class Sottoclasse: public Superclasse {
	private:
		string cognome
	public:
		Sottoclasse(int anno, string nome, string cognome):Superclasse(anno,nome) {
			this->cognome=cognome;
		}
		void metodo(){}
}
```
In questo caso non è necessario dichiarare il costruttore di default, poiché la sottoclasse eredita il costruttore della super classe. L'unico attributo da inizializzare nel costruttore, qualora lo si voglia inizializzare tramite costruttore, in questo caso è *cognome*.

Quando si dichiara una sottoclasse è bene specificare il **public** in modo tale da permettere alla sotto classe di ereditare dalla super classe. Altrimenti ci darà errore in console.

Inoltre gli attributi della sottoclasse vanno impostati come **private** poiché la loro visibilità venga limitata solo alla sottoclasse.

## Ereditarietà dei metodi
I metodi possono essere ereditati in due modi:
- **Overriding**: stesso nome, stesso tipo e stesso numero di argomenti (parametri) al metodo ereditato dalla super classe.
- **Overloading**: stesso nome, ma tipo e numero di argomenti diversi dal metodo ereditato dalla super classe.

Esempio di **Overriding**.
```cpp
class Superclasse {
	protected:
		int anno;
		string nome;
	public:
		Superclasse(){}
		Superclasse(int anno, string nome) {
			this->anno=anno;
			this->nome=nome;
		}
		//metodo su cui eseguire l'overriding
		virtual void metodo1(int parametro1, float parametro2){}
}

class Sottoclasse: public Superclasse {
	private:
		string cognome
	public:
		Sottoclasse(int anno, string nome, string cognome):Superclasse(anno,nome) {
			this->cognome=cognome;
		}
		//metodo sovrascritto
		void metodo1(int parametro1, float parametro2) override {}
}
```
Nell'overriding l'unica cosa che cambia nel metodo sono le istruzioni contenute al suo interno.
Le keyword **virtual** e **override** servono a farci capire quando su un metodo viene eseguito l'overriding.

Esempio di **Overloading**.
```cpp
class Superclasse {
	protected:
		int anno;
		string nome;
	public:
		Superclasse(){}
		Superclasse(int anno, string nome) {
			this->anno=anno;
			this->nome=nome;
		}
		//metodo su cui eseguire l'overloading
		void metodo1(int parametro1, float parametro2){}
}

class Sottoclasse: public Superclasse {
	private:
		string cognome
	public:
		Sottoclasse(int anno, string nome, string cognome):Superclasse(anno,nome) {
			this->cognome=cognome;
		}
		//metodo nella sottoclasse
		string metodo1(string parametro1){}
}
```
Nell'overloading ovviamente oltre a cambiare il tipo o numero di parametri cambiano anche le istruzioni contenute all'interno del metodo.

## Utilizzo della classe nel main di C++ per istanziare oggetti della classe
```cpp
class Superclasse {
	private:
		int anno;
		string nome;
	public:
		Superclasse(){}
		Superclasse(int anno, string nome) {
			this->anno=anno;
			this->nome=nome;
		}
		
		void metodo1(int parametro1, float parametro2){}
}

int main() {
	
	Superclasse oggetto1;
	int annoInInput;
	string nomeInInput;
	int p1;
	float p2;
	
	//Istruzioni di input
	cout<<"Inserire anno: ";
	cin>>annoInInput;
	cout<<"Inserire nome: ";
	cin>>nomeInInput;
	
	//Qui all'oggetto assegnamo il costruttore della classe
	oggetto1=Superclasse(annoInInput,nomeInInput);
	
	//utilizzo di un metodo
	oggetto1.metodo1(p1,p2);
	
	return 0;
}
```

## Aggiunte finali

### I metodi get e set
I metodi **get/set** sono dei metodi definiti dal programmatore che permettono la lettura o scrittura all'interno degli attributi. Sono importanti perché rappresentano il concetto di **incapsulamento**, il quale definisce che l'accesso agli attributi deve avvenire per mezzo dei metodi che sono pubblici, e quindi accedere agli attributi che sono privati.

Esempio
```cpp
class Superclasse {
	private:
		int anno;
		string nome;
	public:	
		void setAnno(int anno) {
			this->anno=anno;
		}
		
		string getNome() {
			return nome;
		}
}

int main() {
	
	Superclasse oggetto1;
	int annoInInput;
	cout<<"Inserire anno: ";
	cin>>annoInInput;
	// scrive l'anno all'interno dell'attributo della classe
	oggetto1.setAnno(annoInInput);
	
	// legge il nome dall'attributo 'nome' della classe
	cout<<"Il nome e' : "<<oggetto1.getNome()<<endl;
	
	return 0;
}
```

# Crediti
Programmazione in C++ a cura di [@TheiPhoneDev](https://github.com/TheiPhoneDev)




