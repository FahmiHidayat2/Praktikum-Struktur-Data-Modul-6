# <h1 align="center">Laporan Praktikum Modul Tipe Data</h1>
<p align="center">Fahmi Hidayat</p>

## Dasar Teori

Linked list merupakan suatu struktur data yang terdiri dari serangkaian node yang saling terhubung. Setiap node menyimpan sebuah elemen data dan referensi atau pointer ke node berikutnya dalam urutan. Ini berbeda dengan array, di mana elemen-elemen data disimpan secara berurutan dalam memori. Linked List memiliki keunggulan dibandingkan Array dalam hal menambahkan dan mengurangi elemennya [1].

### 1. Single Linked List
Single Linked List adalah struktur data linear di mana setiap node memiliki dua bagian utama: data yang menyimpan informasi, dan pointer yang menunjuk ke node berikutnya dalam urutan. Ini membuatnya memori efisien karena hanya memerlukan satu pointer per node. Namun, kelemahannya adalah akses terhadap elemen hanya bisa dilakukan satu arah, dari awal ke akhir, sehingga traversal mundur tidak mungkin dilakukan. Operasi dasarnya meliputi inisialisasi linked list, penambahan dan penghapusan node, serta traversal melalui setiap node.

### 2. Double Linked List
Double Linked List, di sisi lain, adalah struktur data yang mirip, namun setiap node memiliki tambahan pointer yang menunjuk ke node sebelumnya. Ini memungkinkan traversal maju dan mundur, membuatnya lebih fleksibel dalam akses data. Namun, kekurangannya adalah penggunaan memori yang lebih besar karena setiap node memerlukan dua pointer, serta implementasi yang lebih rumit dibandingkan dengan single linked list. Operasinya mirip dengan single linked list, termasuk inisialisasi, penambahan dan penghapusan node, serta traversal baik maju maupun mundur.
## Guided 

### 1. Guided 1

```C++
// Guided 1
#include <iostream>
using namespace std;

///PROGRAM SINGLE LINKED LIST NON-CIRCULAR
//Deklarasi Struct Node
struct Node{
    //komponen/member
    int data;
    Node *next;
};
    Node *head;
    Node *tail;
//Inisialisasi Node
void init(){
    head = NULL;
    tail = NULL;
}
// Pengecekan
bool isEmpty(){
    if (head == NULL)
    return true;
    else
    return false;
}
//Tambah Depan
void insertDepan(int nilai){
    //Buat Node baru
    Node *baru = new Node;
    baru->data = nilai;
    baru->next = NULL;
    if (isEmpty() == true){
        head = tail = baru;
        tail->next = NULL;
    }
    else{
        baru->next = head;
        head = baru;
    }
}
//Tambah Belakang
void insertBelakang(int nilai){
    //Buat Node baru
    Node *baru = new Node;
    baru->data = nilai;
    baru->next = NULL;
    if (isEmpty() == true){
        head = tail = baru;
        tail->next = NULL;
    }
    else{
    tail->next = baru;
    tail = baru;
    }
}
//Hitung Jumlah List
int hitungList(){
    Node *hitung;
    hitung = head;
    int jumlah = 0;
    while( hitung != NULL ){
        jumlah++;
        hitung = hitung->next;
    }
    return jumlah;
}
//Tambah Tengah
void insertTengah(int data, int posisi){
    if( posisi < 1 || posisi > hitungList() ){
        cout << "Posisi diluar jangkauan" << endl;
    }
    else if( posisi == 1){
        cout << "Posisi bukan posisi tengah" << endl;
    }
    else{
        Node *baru, *bantu;
        baru = new Node();
        baru->data = data;
        // tranversing
            bantu = head;
            int nomor = 1;
        while( nomor < posisi - 1 ){
            bantu = bantu->next;
            nomor++;
        }
        baru->next = bantu->next;
        bantu->next = baru;
    }
}
//Hapus Depan
void hapusDepan() {
    Node *hapus;
    if (isEmpty() == false){
        if (head->next != NULL){
            hapus = head;
            head = head->next;
            delete hapus;
        }
        else{
            head = tail = NULL;
        }
    }
    else{
        cout << "List kosong!" << endl;
    }
}
//Hapus Belakang
void hapusBelakang() {
    Node *hapus;
    Node *bantu;
    if (isEmpty() == false){
        if (head != tail){
            hapus = tail;
            bantu = head;
            while (bantu->next != tail){
                bantu = bantu->next;
            }
            tail = bantu;
            tail->next = NULL;
        delete hapus;
        }
        else{
            head = tail = NULL;
        }
    }
    else{
        cout << "List kosong!" << endl;
    }
}
//Hapus Tengah
void hapusTengah(int posisi){
    Node *hapus, *bantu, *bantu2;
    if( posisi < 1 || posisi > hitungList() ){
        cout << "Posisi di luar jangkauan" << endl;
    }
    else if( posisi == 1){
        cout << "Posisi bukan posisi tengah" << endl;
    }
    else{
        int nomor = 1;
        bantu = head;
        while( nomor <= posisi ){
            if( nomor == posisi-1 ){
                bantu2 = bantu;
            }
            if( nomor == posisi ){
                hapus = bantu;
            }
            bantu = bantu->next;
            nomor++;
        }
        bantu2->next = bantu;
    delete hapus;
    }
}
//Ubah Depan
void ubahDepan(int data){
    if (isEmpty() == false){
        head->data = data;
    }
    else{
        cout << "List masih kosong!" << endl;
    }
}
//Ubah Tengah
void ubahTengah(int data, int posisi){
    Node *bantu;
    if (isEmpty() == false){
        if( posisi < 1 || posisi > hitungList() ){
            cout << "Posisi di luar jangkauan" << endl;
        }
        else if( posisi == 1){
            cout << "Posisi bukan posisi tengah" << endl;
        }
        else{
            bantu = head;
            int nomor = 1;
            while (nomor < posisi){
                bantu = bantu->next;nomor++;
            }
            bantu->data = data;
        }
    }
    else{
        cout << "List masih kosong!" << endl;
    }
}
//Ubah Belakang
void ubahBelakang(int data){
    if (isEmpty() == false){
        tail->data = data;
    }
    else{
        cout << "List masih kosong!" << endl;
    }
}
//Hapus List
void clearList(){
    Node *bantu, *hapus;
    bantu = head;
    while (bantu != NULL){
        hapus = bantu;
        bantu = bantu->next;
        delete hapus;
    }
    head = tail = NULL;
    cout << "List berhasil terhapus!" << endl;
}
//Tampilkan List
void tampil(){
    Node *bantu;
    bantu = head;
    if (isEmpty() == false){
        while (bantu != NULL){
            cout << bantu->data << ends;
            bantu = bantu->next;
        }
        cout << endl;
    }
    else{
        cout << "List masih kosong!" << endl;
    }
}
int main(){
    init();
    insertDepan(3);
    tampil();
    insertBelakang(5);
    tampil();
    insertDepan(2);
    tampil();
    insertDepan(1);
    tampil();
    hapusDepan();
    tampil();
    hapusBelakang();
    tampil();
    insertTengah(7,2);
    tampil();
    hapusTengah(2);
    tampil();
    ubahDepan(1);
    tampil();
    ubahBelakang(8);
    tampil();
    ubahTengah(11, 2);
    tampil();

    insertTengah(7,1);
    tampil();
    return 0;
}
```

### 2. Guided 2
```c++
// Guided 2

#include <iostream>
using namespace std;

class Node {
public:
    int data;
    Node* prev;
    Node* next;
};

class DoublyLinkedList {
public:
    Node* head;
    Node* tail;

    DoublyLinkedList() {
        head = NULL;
        tail = NULL;
    }

    void push(int data) {
        Node* newNode = new Node;
        newNode->data = data;
        newNode->prev = NULL;
        newNode->next = head;
        if (head != NULL) {
            head->prev = newNode;
        }
        else {
            tail = newNode;
        }
        head = newNode;
    }

    void pop() {
        if (head == NULL) {
            return;
        }
        Node* temp = head;
        head = head->next;
        if (head != NULL) {
            head->prev = NULL;
        }
        else {
            tail = NULL;
        }
        delete temp;
    }

    bool update(int oldData, int newData) {
        Node* current = head;
        while (current != NULL) {
            if (current->data == oldData) {
                current->data = newData;
                return true;
            }
            current = current->next;
        }
        return false;
    }

    void deleteAll() {
        Node* current = head;
        while (current != NULL) {
            Node* temp = current;
            current = current->next;
            delete temp;
        }
        head = NULL;
        tail = NULL;
    }

    void display() {
        Node* current = head;
        while (current != NULL) {
            cout << current->data << " ";
            current = current->next;
        }
        cout << endl;
    }
};

int main() {
    DoublyLinkedList list;
    while (true) {
        cout << "1. Add data" << endl;
        cout << "2. Delete data" << endl;
        cout << "3. Update data" << endl;
        cout << "4. Clear data" << endl;
        cout << "5. Display data" << endl;
        cout << "6. Exit" << endl;
        int choice;
        cout << "Enter your choice: ";
        cin >> choice;
        switch (choice) {
        case 1: {
            int data;
            cout << "Enter data to add: ";
            cin >> data;
            list.push(data);
            break;
        }
        case 2: {
            list.pop();
            break;
        }
        case 3: {
            int oldData, newData;
            cout << "Enter old data: ";
            cin >> oldData;
            cout << "Enter new data: ";
            cin >> newData;
            bool updated = list.update(oldData, newData);
            if (!updated) {
                cout << "Data not found" << endl;
            }
            break;
        }
        case 4: {
            list.deleteAll();
            break;
        }
        case 5: {
            list.display();
            break;
        }
        case 6: {
            return 0;
        }
        default: {
            cout << "Invalid choice" << endl;
            break;
        }
        }
    }
    return 0;
}
```


## Unguided 

### 1.  Buatlah program menu Single Linked List Non-Circular untuk menyimpan Nama dan usia mahasiswa, dengan menggunakan inputan dari user. Lakukan operasi berikut:

```C++
#include <iostream>
using namespace std;

// Struktur node untuk menyimpan data mahasiswa
struct Node {
    string nama_030;
    int usia_030;
    Node* next;
};

class LinkedList {
private:
    Node* head;

public:
    // Konstruktor
    LinkedList() {
        head = NULL;
    }

    // Fungsi untuk menambahkan node di depan linked list
    void tambahDepan(string nama_030, int usia_030) {
        Node* newNode = new Node;
        newNode->nama_030 = nama_030;
        newNode->usia_030 = usia_030;
        newNode->next = head;
        head = newNode;
    }

    // Fungsi untuk menambahkan node di belakang linked list
    void tambahBelakang(string nama_030, int usia_030) {
        Node* newNode = new Node;
        newNode->nama_030 = nama_030;
        newNode->usia_030 = usia_030;
        newNode->next = NULL;

        if (head == NULL) {
            head = newNode;
            return;
        }

        Node* temp = head;
        while (temp->next != NULL) {
            temp = temp->next;
        }
        temp->next = newNode;
    }

    // Fungsi untuk menampilkan isi linked list
    void tampilkan() {
        Node* temp = head;
        while (temp != NULL) {
            cout << "Nama: " << temp->nama_030 << ", Usia: " << temp->usia_030 << endl;
            temp = temp->next;
        }
    }

    // Fungsi untuk menghapus node dari linked list
    void hapus(string nama_030) {
        Node* temp = head;
        Node* prev = NULL;

        // Cari node yang akan dihapus
        while (temp != NULL && temp->nama_030 != nama_030) {
            prev = temp;
            temp = temp->next;
        }

        // Jika node tidak ditemukan
        if (temp == NULL) {
            cout << "Data dengan nama " << nama_030 << " tidak ditemukan." << endl;
            return;
        }

        // Jika node yang akan dihapus adalah head
        if (prev == NULL) {
            head = temp->next;
            delete temp;
            cout << "Data dengan nama " << nama_030 << " berhasil dihapus." << endl;
            return;
        }

        // Jika node yang akan dihapus bukan head
        prev->next = temp->next;
        delete temp;
        cout << "Data dengan nama " << nama_030 << " berhasil dihapus." << endl;
    }
    
    // Fungsi untuk menyisipkan node di antara dua mahasiswa berdasarkan nama
    void sisipDiAntara(string nama_awal, string nama_akhir, string nama_030, int usia_030) {
        Node* newNode = new Node;
        newNode->nama_030 = nama_030;
        newNode->usia_030 = usia_030;

        Node* temp = head;
        Node* prev = NULL;

        // Cari node dengan nama_awal
        while (temp != NULL && temp->nama_030 != nama_awal) {
            prev = temp;
            temp = temp->next;
        }

        // Jika node tidak ditemukan
        if (temp == NULL) {
            cout << "Data dengan nama " << nama_awal << " tidak ditemukan." << endl;
            return;
        }

        // Jika node dengan nama_awal ditemukan
        prev = temp;
        temp = temp->next;

        // Cari node dengan nama_akhir
        while (temp != NULL && temp->nama_030 != nama_akhir) {
            prev = temp;
            temp = temp->next;
        }

        // Jika node tidak ditemukan
        if (temp == NULL) {
            cout << "Data dengan nama " << nama_akhir << " tidak ditemukan." << endl;
            return;
        }

        // Sisipkan newNode di antara node dengan nama_awal dan nama_akhir
        prev->next = newNode;
        newNode->next = temp;
    }
    
     // Fungsi untuk menambahkan node di awal linked list
    void tambahDiAwal(string nama_030, int usia_030) {
        Node* newNode = new Node;
        newNode->nama_030 = nama_030;
        newNode->usia_030 = usia_030;
        newNode->next = head;
        head = newNode;
    }
    
   // Fungsi untuk mengubah data mahasiswa berdasarkan nama
    void ubahData(string nama_lama, string nama_baru, int usia_baru) {
        Node* temp = head;

        // Cari node dengan nama_lama
        while (temp != NULL && temp->nama_030 != nama_lama) {
            temp = temp->next;
        }

        // Jika node tidak ditemukan
        if (temp == NULL) {
            cout << "Data dengan nama " << nama_lama << " tidak ditemukan." << endl;
            return;
        }

        // Ubah nama dan usia node menjadi nama_baru dan usia_baru
        temp->nama_030 = nama_baru;
        temp->usia_030 = usia_baru;
        cout << "Data mahasiswa berhasil diubah." << endl;
    }
};

int main() {
    LinkedList list;
    string nama_030;
    int usia_030;


	// Memasukkan data pertama dari pengguna
    cout << "Masukkan nama anda: ";
    getline(cin, nama_030);
    cout << "Masukkan usia anda: ";
    cin >> usia_030;
    cin.ignore(); // Membersihkan buffer

    // Menambahkan data pertama ke linked list
    list.tambahDepan(nama_030, usia_030);

    // Memasukkan 6 data lagi dari pengguna
    for (int i = 0; i < 7; ++i) {
        cout << "Masukkan nama mahasiswa ke-" << i+1 << ": ";
        getline(cin, nama_030);
        cout << "Masukkan usia mahasiswa ke-" << i+1 << ": ";
        cin >> usia_030;
        cin.ignore(); // Membersihkan buffer

        // Menambahkan data ke linked list
        list.tambahBelakang(nama_030, usia_030);
    }

    // Menampilkan isi linked list
    cout << "\nData Mahasiswa:\n";
    list.tampilkan();

    // Meminta pengguna untuk menghapus data
    cout << "\nMasukkan nama mahasiswa yang ingin dihapus: ";
    getline(cin, nama_030);

    // Menghapus data dari linked list
    list.hapus(nama_030);
    

    // Menampilkan isi linked list setelah penghapusan
    cout << "\nData Mahasiswa setelah penghapusan:\n";
    list.tampilkan();
    
    // Meminta pengguna untuk menyisipkan data di antara dua nama mahasiswa
    string nama_awal, nama_akhir;
    cout << "\nMasukkan nama mahasiswa awal: ";
    getline(cin, nama_awal);
    cout << "Masukkan nama mahasiswa akhir: ";
    getline(cin, nama_akhir);
    cout << "Masukkan nama mahasiswa yang ingin disisipkan: ";
    getline(cin, nama_030);
    cout << "Masukkan usia mahasiswa yang ingin disisipkan: ";
    cin >> usia_030;
    cin.ignore(); 

    // Menyisipkan data di antara dua nama mahasiswa
    list.sisipDiAntara(nama_awal, nama_akhir, nama_030, usia_030);
      // Menampilkan isi linked list setelah penyisipan
    cout << "\nData Mahasiswa setelah penyisipan:\n";
    list.tampilkan();
    
    
    // Memasukkan data pertama dari pengguna
    cout << "Masukkan nama mahasiswa: ";
    getline(cin, nama_030);
    cout << "Masukkan usia mahasiswa: ";
    cin >> usia_030;
    cin.ignore(); 

    // Menambahkan data pertama ke linked list
    list.tambahDiAwal(nama_030, usia_030);
      cout << "\nData Mahasiswa setelah ditambah:\n";
    list.tampilkan();
    
 	// Meminta pengguna untuk mengubah data mahasiswa berdasarkan nama
    string nama_lama;
    int usia_baru;
    cout << "\nMasukkan nama mahasiswa yang ingin diubah: ";
    getline(cin, nama_lama);
    cout << "Masukkan nama baru mahasiswa: ";
    getline(cin, nama_030);
    cout << "Masukkan usia baru mahasiswa: ";
    cin >> usia_baru;

    // Mengubah data mahasiswa berdasarkan nama
    list.ubahData(nama_lama, nama_030, usia_baru);

    // Menampilkan isi linked list setelah pengubahan
    cout << "\nSeluruh Data Mahasiswa:\n";
    list.tampilkan();
    
    

    cout << "" << endl;
    cout << "" << endl;
    return 0;
}
```
Program yang Anda tulis merupakan implementasi dari sebuah linked list untuk menyimpan data mahasiswa, yang terdiri dari nama dan usia. Dalam program ini, sebuah kelas LinkedList dibuat untuk mengelola operasi-operasi dasar terkait linked list, seperti menambahkan node di depan dan di belakang, menampilkan isi linked list, menghapus node berdasarkan nama, menyisipkan node di antara dua nama mahasiswa, menambahkan node di awal, dan mengubah data mahasiswa berdasarkan nama. Setiap node dalam linked list memiliki dua anggota data, yaitu nama dan usia, serta pointer next yang menunjuk ke node berikutnya. Program ini memanfaatkan konsep OOP (Object-Oriented Programming) dengan menggunakan kelas dan objek untuk mengorganisir kode dan menyediakan antarmuka yang lebih bersih untuk pengguna. Dengan menggunakan program ini, pengguna dapat dengan mudah menambah, menghapus, menampilkan, menyisipkan, dan mengubah data mahasiswa dalam linked list sesuai kebutuhan mereka.

### 2. Modifikasi Guided Double Linked List dilakukan dengan penambahan operasi untuk menambah data, menghapus, dan update di tengah / di urutan tertentu yang diminta. Selain itu, buatlah agar tampilannya menampilkan Nama produk dan harga.
```c++
#include <iostream>
using namespace std;

class Node {
public:
    string namaProduk_030; // Nama produk
    int harga_030; // Harga produk
    Node* prev_030;
    Node* next_030;
};

class DoublyLinkedList {
public:
    Node* head_030;
    Node* tail_030;

    DoublyLinkedList() {
        head_030 = NULL;
        tail_030 = NULL;
    }

    // Fungsi untuk menambahkan produk ke awal daftar
    void tambah(string namaProduk_030, int harga_030) {
        Node* newNode_030 = new Node;
        newNode_030->namaProduk_030 = namaProduk_030;
        newNode_030->harga_030 = harga_030;
        newNode_030->prev_030 = NULL;
        newNode_030->next_030 = head_030;
        if (head_030 != NULL) {
            head_030->prev_030 = newNode_030;
        } else {
            tail_030 = newNode_030;
        }
        head_030 = newNode_030;
    }

    // Fungsi untuk menambahkan produk setelah produk tertentu
    void tambahSetelah(string namaProduk_030, int harga_030, string namaProdukSebelumnya_030) {
        Node* current_030 = head_030;
        while (current_030 != NULL && current_030->namaProduk_030 != namaProdukSebelumnya_030) {
            current_030 = current_030->next_030;
        }
        if (current_030 != NULL) {
            Node* newNode_030 = new Node;
            newNode_030->namaProduk_030 = namaProduk_030;
            newNode_030->harga_030 = harga_030;
            newNode_030->prev_030 = current_030;
            newNode_030->next_030 = current_030->next_030;
            if (current_030->next_030 != NULL) {
                current_030->next_030->prev_030 = newNode_030;
            } else {
                tail_030 = newNode_030;
            }
            current_030->next_030 = newNode_030;
        } else {
            cout << "Produk sebelumnya tidak ditemukan" << endl;
        }
    }

    // Fungsi untuk menghapus produk dari awal daftar
    void hapus() {
        if (head_030 == NULL) {
            return;
        }
        Node* temp_030 = head_030;
        head_030 = head_030->next_030;
        if (head_030 != NULL) {
            head_030->prev_030 = NULL;
        } else {
            tail_030 = NULL;
        }
        delete temp_030;
    }

    // Fungsi untuk mengupdate nama produk dan harga berdasarkan nama produk lama
    bool update(string namaProdukLama_030, string namaProdukBaru_030, int hargaBaru_030) {
        Node* current_030 = head_030;
        while (current_030 != NULL) {
            if (current_030->namaProduk_030 == namaProdukLama_030) {
                current_030->namaProduk_030 = namaProdukBaru_030;
                current_030->harga_030 = hargaBaru_030;
                return true;
            }
            current_030 = current_030->next_030;
        }
        return false;
    }

    // Fungsi untuk menghapus produk berdasarkan nama produk
    void hapusBerdasarkanNama(string namaProduk_030) {
        Node* current_030 = head_030;
        while (current_030 != NULL && current_030->namaProduk_030 != namaProduk_030) {
            current_030 = current_030->next_030;
        }
        if (current_030 != NULL) {
            if (current_030->prev_030 != NULL) {
                current_030->prev_030->next_030 = current_030->next_030;
            } else {
                head_030 = current_030->next_030;
            }
            if (current_030->next_030 != NULL) {
                current_030->next_030->prev_030 = current_030->prev_030;
            } else {
                tail_030 = current_030->prev_030;
            }
            delete current_030;
        } else {
            cout << "Produk tidak ditemukan" << endl;
        }
    }

    // Fungsi untuk menghapus semua produk dari daftar
    void hapusSemua() {
        Node* current_030 = head_030;
        while (current_030 != NULL) {
            Node* temp_030 = current_030;
            current_030 = current_030->next_030;
            delete temp_030;
        }
        head_030 = NULL;
        tail_030 = NULL;
    }

    // Fungsi untuk menampilkan daftar produk beserta harga
    void tampilkan() {
        Node* current_030 = head_030;
        cout << "Nama Produk\tHarga" << endl;
        while (current_030 != NULL) {
            cout << current_030->namaProduk_030 << "\t" << current_030->harga_030 << endl;
            current_030 = current_030->next_030;
        }
        cout << endl;
    }
};

int main() {
    DoublyLinkedList list_030;

    // Menambahkan produk awal ke daftar
    list_030.tambah("Originote", 60000);
    list_030.tambah("Somethinc", 150000);
    list_030.tambah("Skintific", 100000);
    list_030.tambah("Wardah  ", 50000);
    list_030.tambah("Hanasui ", 30000);

    // Menampilkan produk awal
    cout << "Daftar Produk Awal:" << endl;
    list_030.tampilkan();

    // Menu operasi
    while (true) {
        cout << "Toko Skincare Purwokerto" << endl;
        cout << "1. Tambah Data" << endl;
        cout << "2. Hapus Data" << endl;
        cout << "3. Update Data" << endl;
        cout << "4. Tambah Data Urutan Tertentu" << endl;
        cout << "5. Hapus Data Urutan Tertentu" << endl;
        cout << "6. Hapus Seluruh Data" << endl;
        cout << "7. Tampilkan Data" << endl;
        cout << "8. Exit" << endl;

        int pilihan_030;
        cout << "Masukkan pilihan Anda: ";
        cin >> pilihan_030;

        switch (pilihan_030) {
            case 1: {
                string namaProduk_030;
                int harga_030;
                cout << "Masukkan nama produk: ";
                cin >> namaProduk_030;
                cout << "Masukkan harga: ";
                cin >> harga_030;
                list_030.tambah(namaProduk_030, harga_030);
                break;
            }
            case 2: {
                string namaProduk_030;
                cout << "Masukkan nama produk yang ingin dihapus: ";
                cin >> namaProduk_030;
                list_030.hapusBerdasarkanNama(namaProduk_030);
                break;
            }
            case 3: {
                string namaProdukLama_030, namaProdukBaru_030;
                int hargaBaru_030;
                cout << "Masukkan nama produk yang ingin diupdate: ";
                cin >> namaProdukLama_030;
                cout << "Masukkan nama produk baru: ";
                cin >> namaProdukBaru_030;
                cout << "Masukkan harga baru: ";
                cin >> hargaBaru_030;
                bool berhasil_030 = list_030.update(namaProdukLama_030, namaProdukBaru_030, hargaBaru_030);
                if (!berhasil_030) {
                    cout << "Data tidak ditemukan" << endl;
                }
                break;
            }
            case 4: {
                string namaProduk_030, namaProdukSebelumnya_030;
                int harga_030;
                cout << "Masukkan nama produk yang ingin ditambahkan: ";
                cin >> namaProduk_030;
                cout << "Masukkan harga: ";
                cin >> harga_030;
                cout << "Masukkan nama produk sebelumnya: ";
                cin >> namaProdukSebelumnya_030;
                list_030.tambahSetelah(namaProduk_030, harga_030, namaProdukSebelumnya_030);
                break;
            }
            case 5: {
                // Case 5: Hapus Data Urutan Tertentu
                break;
            }
            case 6: {
                list_030.hapusSemua();
                break;
            }
            case 7: {
                list_030.tampilkan();
                break;
            }
            case 8: {
                return 0;
            }
            default: {
                cout << "Pilihan tidak valid" << endl;
                break;
            }
        }
    }
    
    cout << "" << endl;
    cout << "" << endl;
    return 0;
}
```
Program diatas merupakan implementasi dari Doubly Linked List untuk menyimpan data produk, yang terdiri dari nama produk dan harga. Dalam program ini, dua kelas utama digunakan, yaitu kelas Node dan kelas DoublyLinkedList. Kelas Node merepresentasikan setiap node dalam linked list, yang memiliki anggota data untuk menyimpan nama produk, harga, serta pointer ke node sebelumnya dan node selanjutnya. Kelas DoublyLinkedList digunakan untuk mengelola operasi-operasi pada linked list, seperti menambahkan produk ke awal atau setelah produk tertentu, menghapus produk berdasarkan nama, mengupdate data produk, menghapus semua produk, dan menampilkan seluruh daftar produk. Program ini memungkinkan pengguna untuk melakukan berbagai operasi terhadap daftar produk, seperti menambah, menghapus, mengupdate, dan menampilkan data, sesuai dengan pilihan yang mereka buat dalam menu yang disediakan. Dengan menggunakan program ini, pengguna dapat dengan mudah mengelola daftar produk mereka secara dinamis dan efisien.
## Kesimpulan
Praktikum kali ini membahas tentang single linked list yang merupakan suatu bentuk struktur data yang berisi kumpulan data yang disebut sebagai node yang tersusun secara sekuensial kemudian Double Linked List yang merupakan struktur data Linked List yang mirip dengan Single Linked List, namun dengan tambahan satu pointer tambahan pada setiap simpul yaitu pointer prev yang menunjuk ke simpul sebelumnya
## Referensi
[1] Hermawan Wijaya, Wibisono Sukmo Wardhono, Issa Arwani, "Implementasi Linked List pada Interaksi Antar Marker Augmented Reality untuk Operand dan Operator Aritmatika", Jurnal Pengembangan Teknologi Informasi dan Ilmu Komputer, 2018.
