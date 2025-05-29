#include <iostream>
#include <fstream>
#include <string>
#include <cstdio> // pentru remove
using namespace std;

//  Creează un fișier nou (dacă nu există)
void creeazaFisier(const string& numeFisier) {
    ofstream fisier(numeFisier);
    if (!fisier) {
        cout << "Eroare la crearea fisierului.\n";
        return;
    }
    cout << "Fisierul '" << numeFisier << "' a fost creat cu succes.\n";
    fisier.close();
}

//  Citește conținutul fișierului
void citesteFisier(const string& numeFisier) {
    ifstream fisier(numeFisier);
    if (!fisier) {
        cout << "Eroare: fisierul nu exista sau nu poate fi deschis.\n";
        return;
    }

    cout << "\n--- Continutul fisierului ---\n";
    string linie;
    while (getline(fisier, linie)) {
        cout << linie << endl;
    }
    cout << "------------------------------\n";
    fisier.close();
}

//  Modifică (suprascrie) conținutul fișierului
void modificaFisier(const string& numeFisier) {
    ofstream fisier(numeFisier);
    if (!fisier) {
        cout << "Eroare la deschiderea fisierului pentru scriere.\n";
        return;
    }

    cout << "Introdu textul care va fi scris in fisier (Enter pe o linie goala pentru a termina):\n";
    string linie;
    while (true) {
        getline(cin, linie);
        if (linie.empty()) break;
        fisier << linie << endl;
    }

    fisier.close();
    cout << "Fisierul a fost modificat.\n";
}

//  Șterge fișierul
void stergeFisier(const string& numeFisier) {
    if (remove(numeFisier.c_str()) == 0) {
        cout << "Fisierul '" << numeFisier << "' a fost sters cu succes.\n";
    }
    else {
        cout << "Eroare la stergerea fisierului (poate nu exista).\n";
    }
}

int main() {
    int optiune;
    string numeFisier;

    do {
        cout << "\n=== Sistem Gestiune Fisiere ===\n";
        cout << "1. Creeaza fisier\n";
        cout << "2. Citeste fisier\n";
        cout << "3. Modifica fisier\n";
        cout << "4. Sterge fisier\n";
        cout << "0. Iesire\n";
        cout << "Alege o optiune: ";
        cin >> optiune;
        cin.ignore(); // eliminăm newline-ul din buffer

        if (optiune >= 1 && optiune <= 4) {
            cout << "Introdu numele fisierului: ";
            getline(cin, numeFisier);
        }

        switch (optiune) {
        case 1:
            creeazaFisier(numeFisier);
            break;
        case 2:
            citesteFisier(numeFisier);
            break;
        case 3:
            modificaFisier(numeFisier);
            break;
        case 4:
            stergeFisier(numeFisier);
            break;
        case 0:
            cout << "La revedere!\n";
            break;
        default:
            cout << "Optiune invalida.\n";
        }

    } while (optiune != 0);

    return 0;
}
