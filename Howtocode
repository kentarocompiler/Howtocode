#include <iostream> 
#include <string>
#include <iomanip>
#include <fstream>
#include <vector>
#include <cstdlib> // เพิ่มเพื่อใช้ system("cls")

#include <nlohmann/json.hpp>

using json = nlohmann::json;
using namespace std;

//================= โครงสร้างข้อมูล =================
struct TableOrder {
    vector<string> List;
    vector<int> Price;
    vector<int> Amount;
    int count = 0;
    int total = 0;
};

//================= Global variables =================
string food;
int Num;
int table = 0;
int price[10];
int menu;
int more;
int amount;
int check;

vector<TableOrder> TABLE; //จำนวนโต๊ะ
vector<int> useTable;





//=======================================================================     prototypes      ===========================================================================
void home();

//ALL customer function
void customer();
void selectTable();
void menuu();
int moree();
void showBill();

//ALL employee function
void employ();

//ALL Host function
void Host();
void checktable();
void Bestselling();
void payslip(int tableID);
void manageTables();

void backtohome();

//ALL Json function
//void viewSavedData();
void saveData();
void loadData();
void resetData();

//trap error
int Helpercode(int min, int max);

//======================================================================================================================================================================




void home() {
    // ล้างหน้าจอก่อนแสดงเมนูหลักเสมอ
    system("cls");
    cout << "\n============================================================" << endl;
    cout << "|                                                          |" << endl;
    cout << "|          >>> RESTAURANT MANAGEMENT SYSTEM <<<            |" << endl;
    cout << "|                                                          |" << endl;
    cout << "============================================================" << endl;
    cout << "|                                                          |" << endl;
    cout << "|   0. EXIT                                                |" << endl;
    cout << "|   1. CUSTOMER                                            |" << endl;
    cout << "|   2. EMPLOYEE                                            |" << endl;
    cout << "|   3. HOST / ADMIN                                        |" << endl;
    cout << "|                                                          |" << endl;
    cout << "|                                                          |" << endl;
    cout << "|                                                          |" << endl;
    cout << "============================================================" << endl;
    cout << "SELECT NUMBER >> ";
    cin >> Num;
}



//ฟังก์ชันนี้เอาไว้ดักจากผูู้ใช้พิมไปเรื่อย,ถ้าใช่(int)จะคืนค่าเป้นTrue แล้วก็ออกลูป แต่ถ้าไม่ใช่(int)จะคืนค่าเป้นfalseแล้ววนลูปใหม่
int Helpercode(int min, int max) {
    int input;
    while (!(cin >> input) || input < min || input > max) {
        cout << "Invalid! Enter " << min << "-" << max << " >> ";
        cin.clear(); cin.ignore(1000, '\n');
    }
    return input;
}



//กลับไปหน้าหลัก กับ เปลี่ยนโต๊ะ
void backtohome() {
    cout << endl;
    cout << ">>> 0. BACK TO HOME <<<" << endl;
    cout << ">>> 9. CHANGE TABLE <<< " << endl;
    cout << endl;
    cout << "SELECT OPTION >> ";
}



//ให้ลูกค้าเลือกโต๊ะได้หรือจะกลับไปหน้าหลักก็ได้
void selectTable() {
    while (true) {
        system("cls"); // ล้างหน้าจอ
        cout << endl << endl;
        cout << "================== SELECT TABLE ==================" << endl;

        for (int i = 1; i < TABLE.size(); i++) {

            string status = "";
            if (TABLE[i].total == -1) status = "[RESERVED]";
            else if (TABLE[i].count > 0) status = "[FULL]";

            cout << "  (" << i << ") TABLE " << i << " " << status << endl;
        }
        cout << "--------------------------------------------------" << endl;
        cout << " 0. BACK TO HOME " << endl;
        cout << "--------------------------------------------------" << endl;
        cout << "CHOOSE YOUR TABLE >> ";



        if (!(cin >> table)) {
            cout << "\n---------- PLEASE ENTER NUMBERS ONLY ----------" << endl;
            cin.clear();
            cin.ignore(1000, '\n');
            system("pause"); // หยุดรอให้เห็น error ก่อนรี
            continue;
        }
         if (table >= 1 && table < TABLE.size()) {
            if (TABLE[table].total == -1) {
                cout << "\n!!! THIS TABLE IS RESERVED. PLEASE CHOOSE ANOTHER !!!" << endl;
                system("pause");
                continue; // วนกลับไปเลือกใหม่
            }
            if (TABLE[table].count > 0) {
                cout << "\n!!! THIS TABLE IS CURRENTLY OCCUPIED (NOT AVAILABLE) !!!" << endl;
                system("pause");
                continue; // วนกลับไปเลือกใหม
            }
            useTable[table]++;
            break;
        }

         else if (table == 0) {
             table = 0; // มั่นใจว่าค่า table เป็น 0 จริงๆ ก่อนกลับออกไป
             break;
         }
         else {
             cout << "\n---------- INVALID TABLE NUMBER ----------" << endl;
             system("pause");
         }
    }
}






void customer() {
    while (true) {
        if (table == 0) {
            selectTable(); //ถ้ายังไม่ได้เลือกโต๊ะหรือ table == 0 โปรแกรมจะบังคับให้กลับไปเลือกโต๊ะใหม่
            if (table == 0) return; // ถ้าเลือกเลข 0 จะกลับไปหน้าหลัก
        }

        system("cls"); // ล้างหน้าจอ
        cout << "\nTABLE: " << table << endl;
        cout << "========================================" << endl;
        cout << "            ORDER CATEGORIES            " << endl;
        cout << "========================================" << endl;
        cout << "1. RECOMMENDED MENU " << endl;
        cout << "2. MAIN COURSES" << endl;
        cout << "3. BEVERAGES" << endl;
        cout << "4. DESSERTS" << endl;
        cout << "----------------------------------------" << endl;
        cout << "0. HOME     |   9. CHANGE TABLE " << endl;
        cout << "----------------------------------------" << endl;
        cout << "SELECT MENU >> ";

        if (!(cin >> menu)) { //ถ้าใช่(int)คืนค่าเป้นTrueแล้วเจอนิเศษกลายเป้นfalseเลยข้าม แต่ถ้าไม่ใช่(int)คืนค่าเป็นfalseแล้วเจอนิเศษกลายเป้นTrueเลยทำเงื่อนไขในif
            cout << ">>> INVALID INPUT! <<<" << endl;
            cin.clear();
            cin.ignore(1000, '\n');
            system("pause");
            continue;
        }

        if (menu == 0) {
            return; //ถ้าเลือก 0 จบการทำงานฟังก์ชันนี้กลับไปหาฟังก์ชันต้นทางที่เข้ามา
        }

        if (menu == 9) { //ถ้าเลือก 9 จะรีเซ็ตเลขโต๊ะเป้น 0 แล้วไปวนข้างบนใหม่พอเจอแล้วโปรแกรมจะบังคับไปหน้าเลือกโต๊ะ(selectTable)
            table = 0;
            continue;
        }

        if (menu >= 1 && menu <= 4) {
            menuu();
            cout << "AMOUNT >> ";
            while (!(cin >> amount) || amount <= 0) {
                cout << "INVALID AMOUNT! : ";
                cin.clear();
                cin.ignore(1000, '\n');
            }
            //ส่งข้อมูลมาจากฟังก์ชันเมนู
            TABLE[table].List.push_back(food);
            TABLE[table].Price.push_back(price[menu]);//price[menu] - ราคาของที่พึ่งเลือกไปจากฟังก์ชันเมนู, Price - เอาข้อมูลจาก price[menu]มาเก็บไว้
            TABLE[table].Amount.push_back(amount);
            TABLE[table].total += (price[menu] * amount);
            TABLE[table].count++;
            //table - เลขโต๊ะ
            //TABLE - จำนวนโต๊ะ



            cout << endl;
            cout << ">> ADDED : " << food << " x" << amount << " - " << (price[menu] * amount) << " BAHT <<" << endl;
        }
        else {
            cout << ">>> INVALID CATEGORY! <<<" << endl;
            system("pause"); continue;
        }

        if (moree() == 0) return;
    }
}




void menuu() {
    int item, size;
    system("cls"); // ล้างจอแสดงรายการอาหารย่อย
    if (menu == 1) {
        cout << "\n==================== RECOMMENDED ====================" << endl;
        cout << " 1) SPICY TOM YUM GOONG SOUP WITH RICE   80/85 BTH" << endl;
        cout << " 2) MANGO STICKY RICE                    50/55 BTH" << endl;
        cout << " 3) SOM TAM THAI                         50/60 BTH" << endl;
        cout << "-----------------------------------------------------" << endl;
        cout << "SELECT MENU (1-3) >> ";
        item = Helpercode(1, 3);

        if (item == 1) {
            food = "SPICY TOM YUM GOONG SOUP WITH RICE";
            cout << "SELECT SIZE (1) NORMAL 80 / (2) EXTRA 85 >> ";
            size = Helpercode(1, 2);
            if (size == 1) price[menu] = 80;
            else price[menu] = 85;

        }
        else if (item == 2) {
            food = "MANGO STICKY RICE";
            cout << "SELECT SIZE (1) NORMAL 50 / (2) EXTRA 55 >> ";
            size = Helpercode(1, 2);
            if (size == 1) price[menu] = 50;
            else price[menu] = 55;

        }
        else {
            food = "SOM TAM THAI";
            cout << "SELECT SIZE (1) NORMAL 50 / (2) EXTRA 60 >> ";
            size = Helpercode(1, 2);
            if (size == 1) price[menu] = 50;
            else price[menu] = 60;

        }
    }
    else if (menu == 2) {
        cout << "\n========== MAIN COURSES ==========" << endl;
        cout << " 1) FRIED PORK RICE      30/35 BTH" << endl;
        cout << " 2) FRIED CHICKEN RICE   30/35 BTH" << endl;
        cout << "----------------------------------" << endl;
        cout << "SELECT MENU (1-2) >> ";
        item = Helpercode(1, 2);

        if (item == 1) food = "FRIED PORK RICE";
        else food = "FRIED CHICKEN RICE";


        cout << "SELECT SIZE (1) NORMAL 30 / (2) EXTRA 35 >> ";
        size = Helpercode(1, 2);
        if (size == 1) price[menu] = 30;
        else price[menu] = 35;

    }
    else if (menu == 3) {
        cout << "\n=============== BEVERAGES ===============" << endl;
        cout << " 1) WATER                          10 BTH " << endl;
        cout << " 2) SOFT DRINK                     20 BTH " << endl;
        cout << "-----------------------------------------" << endl;
        cout << "SELECT MENU (1-2) >> ";
        item = Helpercode(1, 2);
        if (item == 1) {
            food = "WATER";
            price[menu] = 10;
        }
        else {
            food = "SOFT DRINK";
            price[menu] = 20;
        }
    }
    else if (menu == 4) {
        cout << "\n================ DESSERTS ===============" << endl;
        cout << " 1) ICE CREAM                      15 BTH" << endl;
        cout << " 2) CAKE                           30 BTH" << endl;
        cout << "-----------------------------------------" << endl;
        cout << "SELECT MENU (1-2) >> ";
        item = Helpercode(1, 2);

        if (item == 1) {
            food = "ICE CREAM";
            price[menu] = 15;
        }
        else {
            food = "CAKE";
            price[menu] = 30;
        }
    }
}




int moree() {
    while (true) {
        cout << "\nMORE ORDER? (1) YES / (2) NO" << endl;
        backtohome();
        cin >> more;
        if (more == 1) {
            return 1;
        }
        if (more == 2) {
            showBill();
            system("pause"); // พักหน้าจอให้ดูบิลก่อนกลับ
            return 0;
        }
        if (more == 0) {
            return 0;
        }
        if (more == 9) {
            table = 0; //รีเซ๊ตโต๊ะแล้วกลับไปวนใหม่ในฟังก์ชันcustomer
            return 1;
        }
    }
}




void showBill() {
    system("cls");
    cout << "\n============ BILL SUMMARY (TABLE " << table << ") ===========" << endl;
    for (int i = 0; i < TABLE[table].count; i++) {
        cout << i + 1 << ". " << TABLE[table].List[i] << " x" << TABLE[table].Amount[i] << " = " << TABLE[table].Price[i] * TABLE[table].Amount[i] << " BAHT" << endl;
    }
    cout << "TOTAL PRICE : " << TABLE[table].total << " BAHT" << endl;
    cout << "-------------------------------------\n" << endl;
}




void employ() {
    while (true) {
        system("cls");
        cout << "\n====================================================================" << endl;
        cout << "                        TABLE STATUS DASHBOARD                       " << endl;
        cout << "====================================================================" << endl;
        cout << left << setw(8) << "TABLE" << setw(20) << "STATUS" << setw(12) << "ORDERS" << setw(15) << "TOTAL(BAHT)" << endl;
        cout << "--------------------------------------------------------------------\n";

        for (int i = 1; i < TABLE.size(); i++) {
            string status;
            if (TABLE[i].total == -1) status = "RESERVED";
            else if (TABLE[i].count > 0) status = "NOT AVAILABLE";
            else status = "AVAILABLE";


            cout << left << setw(8) << i << setw(20) << status;

            if (TABLE[i].total == -1) {
                cout << setw(12) << "-" << right << setw(10) << "-" << endl;
            }
            else {
                cout << setw(12) << TABLE[i].count << right << setw(10) << TABLE[i].total << endl;
            }

        }

        cout << "--------------------------------------------------------------------\n";
        cout << "SELECT TABLE TO MANAGE (0 = BACK) >> ";
        cin >> check;


        if (check == 0) return;
        if (check < 1 || check >= TABLE.size()) {
            cout << "\n!!! INVALID TABLE NUMBER !!!\n";
            system("pause");
            continue;
        }

        if (TABLE[check].count == 0 && TABLE[check].total != -1) {
            cout << "\nTable " << check;
            cout << " is Empty." << endl;
            cout << "1. Reserve Table" << endl;
            cout << "0. Back" << endl;
            cout << "Select >> ";
            int reserve;
            cin >> reserve;

            if (reserve == 1) {
                TABLE[check].total = -1;
            }

        }
        else if (TABLE[check].total == -1) {
            cout << "\nTABLE " << check << endl;
            cout << " RESERVED." << endl;
            cout << "1. Unreserve" << endl;
            cout << "0. Back" << endl;
            cout << "Select >> ";
            int unreserve;
            cin >> unreserve;

            if (unreserve == 1) {
                TABLE[check].total = 0;
            }

        }
        else if (TABLE[check].count > 0) {
            cout << "\nTABLE " << check << endl;
            cout << "\n>>> DETAILS <<< :\n" << endl;
            for (int i = 0; i < TABLE[check].count; i++) {
                cout << i + 1 << ". " << TABLE[check].List[i] << " x" << TABLE[check].Amount[i] << endl;
            }
            cout << "TOTAL: " << TABLE[check].total << " BAHT" << endl;
            cout << "\nCLEAR TABLE? (1 = YES / 0 = NO) >> ";

            int clear;
            cin >> clear;
            if (clear == 1) {
                TABLE[check].List.clear();
                TABLE[check].Price.clear();
                TABLE[check].Amount.clear();
                TABLE[check].count = 0;
                TABLE[check].total = 0;
            }
        }
    }
}




void Host() {
    int choose;
    while (true) {
        system("cls"); // ล้างจอเข้าหน้า Admin
        cout << "==================================================" << endl;
        cout << "                 HOST CONTROL PANEL               " << endl;
        cout << "==================================================" << endl;
        cout << "  1.TABLE USAGE" << endl;
        cout << "  2.BEST SELLING MENU" << endl;
        cout << "  3.DAILY PAYSLIP REPORT" << endl;
        cout << "  4.RESET DATA" << endl;
        cout << "  5.MANAGE TABLE " << endl;
        cout << "--------------------------------------------------" << endl;
        cout << "  [0] BACK TO MAIN MENU" << endl;
        cout << "==================================================" << endl;
        cout << "SELECT OPTION >> ";
        cin >> choose;


        if (choose == 0) return;
        else if (choose == 1) {
            checktable();
            system("pause");
        }
        else if (choose == 2) {
            Bestselling();
            system("pause");
        }
        else if (choose == 3) {
            int tableID;
            cout << "ENTER TABLE ID: ";
            cin >> tableID;
            if (tableID >= 1 && tableID < TABLE.size()) {
                payslip(tableID);
            }
            else {
                cout << "INVALID ID!" << endl;
            }
            system("pause");
        }

        else if (choose == 4) {
            resetData();
            //cout << ">>> DATA RESET <<<" << endl; 
            system("pause");
        }
        else if (choose == 5) {
            manageTables();
            system("pause");
        }
    }
}



void checktable() {
    for (int i = 1; i < (int)TABLE.size(); i++)
        cout << "Table " << i << " used " << useTable[i] << " times" << endl;
}




void Bestselling() {

    if (TABLE.size() <= 1) {
        cout << "No data" << endl;
        return;
    }
    vector<string> name;
    vector<int> totalQty;
    for (int t = 1; t < TABLE.size(); t++) {
        for (int i = 0; i < TABLE[t].count; i++) {
            string item = TABLE[t].List[i]; int qty = TABLE[t].Amount[i];
            bool found = false;

            for (int j = 0; j < (int)name.size(); j++) {
                if (name[j] == item) {
                    totalQty[j] += qty;
                    found = true;
                    break;
                }
            }
            if (!found) {
                name.push_back(item);
                totalQty.push_back(qty);
            }
        }
    }
    if (name.empty()) {
        cout << "No orders yet" << endl;
        return;
    }

    int maxIdx = 0;

    for (int i = 1; i < (int)totalQty.size(); i++) {
        if (totalQty[i] > totalQty[maxIdx]) maxIdx = i;
    }

    cout << "\n===== BEST SELLING MENU =====\n" << name[maxIdx] << " | Sold: " << totalQty[maxIdx] << endl;

}



void payslip(int tableID) {
    if (TABLE[tableID].count <= 0) {
        cout << "\n[!] Table " << tableID << " has no orders." << endl;
        return;
    }

    // หัวใบเสร็จแบบเรียบง่าย ใช้ขีดธรรมดา
    cout << "\n------------------------------------------" << endl;
    cout << "            RECEIPT - TABLE " << tableID << endl;
    cout << "------------------------------------------" << endl;

    // หัวข้อคอลัมน์ (ใส่ให้ดูรู้เรื่องว่าอันไหนคืออะไร)
    cout << left << setw(4) << "No."
        << setw(22) << "Menu"
        << setw(6) << "Qty"
        << "Price" << endl;
    cout << "------------------------------------------" << endl;

    // วนลูปแสดงรายการ
    for (int i = 0; i < TABLE[tableID].count; i++) {
        // สร้าง string มารับชื่อเมนูก่อน
        string menuName = TABLE[tableID].List[i];

        // ถ้าชื่อเมนูยาวเกิน 20 ตัว ให้ตัดทิ้งแล้วเติม .. แทน (ป้องกันบรรทัดเบี้ยว)
        if (menuName.length() > 20) {
            menuName = menuName.substr(0, 17) + "...";
        }

        cout << left << setw(4) << i + 1
            << setw(22) << menuName // พิมพ์ชื่อที่จัดการแล้ว
            << "x" << left << setw(5) << TABLE[tableID].Amount[i]
            << right << setw(7) << (TABLE[tableID].Price[i] * TABLE[tableID].Amount[i])
            << " B." << endl;
    }

    // สรุปยอด
    cout << "------------------------------------------" << endl;
    cout << " TOTAL AMOUNT:" << right << setw(20) << TABLE[tableID].total << " Baht" << endl;
    cout << "------------------------------------------" << endl;

}




void manageTables() {
    int choice;
    cout << "\n--- TABLE MANAGEMENT ---" << endl;
    cout << "1. Add 1 Table | 2. Remove Last | 0. Back" << endl;
    cout << "SELECT >> ";
    cin >> choice;

    if (choice == 1) {
        TABLE.push_back(TableOrder());
        useTable.push_back(0);
        cout << ">>> ADDED TABLE " << TABLE.size() - 1 << " <<<" << endl;
    }
    else if (choice == 2 && TABLE.size() > 2) {
        if (TABLE.back().count == 0) {
            TABLE.pop_back();
            useTable.pop_back();
            cout << ">>> REMOVED <<<" << endl;
        }
        else cout << "!!! TABLE NOT EMPTY !!!" << endl;
    }
}




void saveData() {
    json j;
    for (int i = 1; i < (int)TABLE.size(); i++) {
        j["useTable"][to_string(i)] = useTable[i];
        json tJ; tJ["count"] = TABLE[i].count; tJ["total"] = TABLE[i].total;
        for (int k = 0; k < TABLE[i].count; k++) {
            tJ["orders"].push_back({ {"item", TABLE[i].List[k]}, {"price", TABLE[i].Price[k]}, {"qty", TABLE[i].Amount[k]} });
        }
        j["tables"][to_string(i)] = tJ;
    }
    ofstream file("database.json"); file << j.dump(4);
}




void loadData() {
    ifstream file("database.json");
    if (!file.is_open()) { TABLE.resize(6); useTable.assign(6, 0); return; }
    json j; file >> j;
    int savedTableCount = j["tables"].size();
    TABLE.resize(savedTableCount + 1); useTable.resize(savedTableCount + 1);
    for (int i = 1; i < TABLE.size(); i++) {
        string s = to_string(i); useTable[i] = j["useTable"].value(s, 0);
        if (j["tables"].contains(s)) {
            TABLE[i].count = j["tables"][s].value("count", 0);
            TABLE[i].total = j["tables"][s].value("total", 0);
            for (auto& o : j["tables"][s]["orders"]) {
                TABLE[i].List.push_back(o.value("item", ""));
                TABLE[i].Price.push_back(o.value("price", 0));
                TABLE[i].Amount.push_back(o.value("qty", 0));
            }
        }
    }
}





void resetData() {
    int confirm;
    cout << "\n!!! WARNING: RESET ALL DATA !!!" << endl;
    cout << "1. Confirm / 2. Cancel: ";
    cin >> confirm;

    if (confirm == 1) {
        for (int i = 0; i < TABLE.size(); i++) {
            TABLE[i].List.clear(); TABLE[i].Price.clear(); TABLE[i].Amount.clear();
            TABLE[i].count = 0; TABLE[i].total = 0;
        }
        fill(useTable.begin(), useTable.end(), 0);
        cout << ">>> RESET COMPLETED <<<" << endl;
    }
    else cout << ">>> PLEASE CAREFULLY RESET DATA <<<" << endl;
}





int main() {
    loadData();
    while (true) {
        home(); // ฟังก์ชันนี้จะทำ system("cls") ให้เองข้างใน
        if (cin.fail()) {
            cin.clear();
            cin.ignore(1000, '\n');
            continue;
        }
        if (Num == 0) {
            saveData();
            return 0;
        }
        if (Num == 1) {
            table = 0;
            customer();
        }
        else if (Num == 2) {
            string pass;
            cout << "Password: ";
            cin >> pass;
            if (pass == "checkin") employ();
        }
        else if (Num == 3) {
            string pass;
            cout << "Password: ";
            cin >> pass;
            if (pass == "manage") Host();
        }
        else {
            cout << "Input valid error" << endl;
            system("pause");
        }
    }
}
