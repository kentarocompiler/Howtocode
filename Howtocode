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
struct MenuStats {
    string name;
    int totalQty = 0;
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
vector<MenuStats> globalSales; // เก็บยอดขายรวมของทั้งวัน





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
            TABLE[table].total += (price[menu] * amount); //คำนวนราคา * จำนวนอาหาร
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
    int Option2;
    while (true) {
        system("cls");
        cout << "\n====================================================================" << endl;
        cout << "                        TABLE STATUS DASHBOARD                       " << endl;
        cout << "====================================================================" << endl;
        cout << left << setw(8) << "TABLE" << setw(20) << "STATUS" << setw(12) << "ORDERS" << setw(15) << "TOTAL(BAHT)" << endl;
        cout << "--------------------------------------------------------------------\n";

        for (int i = 1; i < TABLE.size(); i++) {
            string status;
            if (TABLE[i].total == -1) status = "RESERVED"; //ถ้าโต๊ะถูกจองแล้ว จะเป้น-1แล้วมาทำเงื่อนไขนี้ เก็บข้อมูลมาจาก cin>>reserve(ถ้าเลือก1) -1แปลว่าโต๊ะไม่ว่างนะ 
            else if (TABLE[i].count > 0) status = "NOT AVAILABLE";//ถ้าโต๊ะถูกนับหรือเคยใช้มาแล้วให้เข้าเงื่อนไขนี้
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


        if (check == 0) return; //จบฟังก์ชันนี้กลับหน้าหลัก
        if (check < 1 || check >= TABLE.size()) {
            cout << "\n!!! INVALID TABLE NUMBER !!!\n";
            system("pause");
            continue;
        }

        if (TABLE[check].count == 0 && TABLE[check].total != -1) {//ถ้าโต๊ะว่างและไม่ถูกจองเข้าเงื่อนไขนี้
            cout << "\nTable " << check;
            cout << " is Empty." << endl;
            cout << "1. Reserve Table" << endl;
            cout << "2. payslip" << endl;
            cout << "0. Back" << endl;
            cout << "Select >> ";
            int reserve;
            cin >> reserve;

            if (reserve == 1) {
                TABLE[check].total = -1;
            }
            else if (reserve == 2) {
                payslip(check);
                system("pause");
            }

        }
        else if (TABLE[check].total == -1) {//ถ้าโต๊ะถูกจองแล้วเข้าเงื่อนไขนี้
            cout << "\nTABLE " << check << endl;
            cout << " RESERVED." << endl;
            cout << "1. Unreserve" << endl;
            cout << "2. payslip" << endl;
            cout << "0. Back" << endl;
            cout << "Select >> ";
            int unreserve;
            cin >> unreserve;

            if (unreserve == 1) {//ถ้าเลือก1ให้โต๊ะกลับมาว่าง
                TABLE[check].total = 0;
            }
            else if (unreserve == 2) {
                payslip(check);
                system("pause");
            }

        }
        else if (TABLE[check].count > 0) {//ถ้าโต๊ะถูกใช้งานหรือนับมาแล้วให้เแสดงข้อมูลในโต๊ะนั้น
            cout << "\nTABLE " << check << endl;
            cout << "\n----------------->>> DETAILS <<< --------------------\n" << endl;
            for (int i = 0; i < TABLE[check].count; i++) {
                cout << i + 1 << ". " << TABLE[check].List[i] << " x" << TABLE[check].Amount[i] << endl;
            }
            cout << "TOTAL: " << TABLE[check].total << " BAHT" << endl;
            cout << "\n-----------------------------------------------------" << endl;
            cout << "1. View Payslip" << endl;
            cout << "2. CLEAR TABLE" << endl;
            int Option2;
            cout << endl << ">> ";
            cin >> Option2;

            if (Option2 == 2) {//ถ้าเลือก1 ให้ล้างข้อมูลของโต๊ะนั้น ทำให้กลายเป้น0
                cout << "\nCLEAR TABLE? (1 = YES / 0 = NO) >> ";
                int confirmClear;
                cout << ":"; cin >> confirmClear;
                if (confirmClear == 1) {
                    TABLE[check].List.clear();
                    TABLE[check].Price.clear();
                    TABLE[check].Amount.clear();
                    TABLE[check].count = 0;
                    TABLE[check].total = 0;
                }
                else {
                    cout << "\n>>> CANCEL <<<" << endl;
                }
            }
            else if (Option2 == 1) {
                payslip(check);
                system("pause");
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
        cout << "  3.RESET DATA" << endl;
        cout << "  4.MANAGE TABLE " << endl;
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
            resetData();//cout << ">>> DATA RESET <<<" << endl; 
            system("pause");
        }
        else if (choose == 4) {
            manageTables();
            system("pause");
        }
    }
}



void checktable() {//เช็คสถานะโต๊ะว่ามีโต๊ะไหนถูกใช้งานบ้าง
    for (int i = 1; i < TABLE.size(); i++)
        cout << "Table " << i << " used " << useTable[i] << " times" << endl;
}




void Bestselling() {
    if (TABLE.size() <= 1) {//เช็คว่ามีโต๊ะมั้ย
        system("cls");
        cout << "\n==================================================" << endl;
        cout << " [!] NO DATA YET... THE KITCHEN IS WAITING! [!] " << endl;
        cout << "==================================================\n" << endl;
        return;
    }

    vector<string> menuName;
    vector<int> totalAmount;


    for (int t = 1; t < TABLE.size(); t++) { // ไล่นับยอดขายจากทุกโต๊ะที่กินไปแล้ว
        for (int i = 0; i < TABLE[t].count; i++) {

            string Item = TABLE[t].List[i]; // ชื่ออาหารที่กำลังเช็ค
            int Qty = TABLE[t].Amount[i];   // จำนวนที่สั่ง
            bool isFound = false;           // เอาไว้เช็คว่าเคยจดชื่อเมนูนี้ไปยัง


            for (int j = 0; j < menuName.size(); j++) {// ค้นหาว่าเคยเขียนชื่อเมนูนี้ลงไปหรือยัง
                if (menuName[j] == Item) { //หาทีละตัวว่าเคยบันทึกไว้มั้ย
                    totalAmount[j] += Qty; // ถ้าเคยจดแล้ว ให้บวกจำนวนเข้าไปเพิ่ม
                    isFound = true;        // ติ๊กถูกว่า "เจอแล้วนะ"
                    break;                 // เจอแล้วก็เลิกหา ข้ามไปเมนูถัดไปได้เลย
                }
            }

            // ถ้าค้นหาแล้วยังไม่เจอ
            if (isFound == false) {
                menuName.push_back(Item);   // เขียนชื่อเมนูใหม่ลงไป
                totalAmount.push_back(Qty); // เขียนจำนวนลงไป
            }
        }
    }

    //เช้คว่ามีคนสั่งอาหารจริงๆมั้ยยหรืออาจจะเปิดโต๊ะไว้แต่ยังไม่สั่ง
    if (menuName.empty()) { //ถ้าโต๊ะว่างให้เข้าเงื่อนไขนี้แล้วจบฟังก์ชัน
        system("cls");
        cout << "\n==================================================" << endl;
        cout << "  [!] NO ORDERS YET... LET'S GET SOME CUSTOMERS!  " << endl;
        cout << "==================================================\n" << endl;
        return;
    }

    //หาว่าเมนูไหนยอดขายเยอะสุด
    int indexBest = 0; //ตั้งให้อันแรกเป้น0ไปก่อนละค่อยๆเทียบเอา

    for (int i = 1; i < totalAmount.size(); i++) {
        if (totalAmount[i] > totalAmount[indexBest]) {// ถ้าเจออ้นที่เยอะกว่าให้เปลี่ยนข้อมูลใหม่
            indexBest = i; // ตำแหน่งเเชมป์คนใหม่
        }
    }

    system("cls");
    cout << "\n==================================================" << endl;
    cout << "   *** THE UNDISPUTED CHAMPION OF THE DAY! *** " << endl;
    cout << "==================================================" << endl;
    cout << "\n";
    cout << "           [ " << menuName[indexBest] << " ] " << endl;
    cout << "             TOTAL SOLD: " << totalAmount[indexBest] << " DISHES!" << endl;
    cout << "\n";
    cout << "       >>> CUSTOMERS ABSOLUTELY LOVE THIS! <<<    " << endl;
    cout << "\n==================================================" << endl;
}



void payslip(int tableID) {
    if (TABLE[tableID].count <= 0) {
        cout << "\n[!] Table " << tableID << " has no orders." << endl;
        return;
    }

    cout << "\n------------------------------------------" << endl;
    cout << "            RECEIPT - TABLE " << tableID << endl;
    cout << "------------------------------------------" << endl;


    cout << left << setw(4) << "No."
        << setw(22) << "Menu"
        << setw(6) << "Qty"
        << "Price" << endl;
    cout << "------------------------------------------" << endl;


    for (int i = 0; i < TABLE[tableID].count; i++) {
        string menuName = TABLE[tableID].List[i];

        // ถ้าชื่อเมนูยาวเกิน20ตัว เติมจุดจุดเเทนนะ กันเบี้ยว
        if (menuName.length() > 20) {
            menuName = menuName.substr(0, 17) + "...";
        }

        cout << left << setw(4) << i + 1 << setw(22) << menuName
            << "x" << left << setw(5) << TABLE[tableID].Amount[i]
            << right << setw(7) << (TABLE[tableID].Price[i] * TABLE[tableID].Amount[i])
            << " B." << endl;
    }

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
        TABLE.push_back(TableOrder());// เพิ่มข้อมูลโต๊ะใหม่เปล่าๆ ต่อท้ายเข้าไปในระบบ
        useTable.push_back(0);// ตั้งค่าว่าโต๊ะนี้ยังไม่ได้ใช้งาน
        cout << ">>> ADDED TABLE " << TABLE.size() - 1 << " <<<" << endl;
    }
    else if (choice == 2 && TABLE.size() > 2) {//ถ้าเลือก2 และ จำนวนโต๊ะมากกว่า2 ให้เข้าเงื่อนไขนี้เพราะถ้าโต๊ะน้อยกว่า2 มันจะไม่มีให้เลือกแล้วโปรแกรมจะพังเลยต้องมีอย่างน้อย2โต๊ะ(ไม่นับเลข0)
        if (TABLE.back().count == 0) { //เช็คก่อนว่าโต๊ะตัวสุดท้ายที่จะลบเนี้ยว่างอยู่มั้ย(ไม่มีรายการอาหาร)
            TABLE.pop_back(); //ลบข้อมูลโต๊ะตัวสุดท้ายทิ้ง
            useTable.pop_back(); //ลบสถิติการใช้งานของโต๊ะตัวสุดท้ายทิ้ง
            cout << ">>> REMOVED <<<" << endl;
        }
        else cout << "TABLE NOT EMPTY!" << endl;
    }
    else if (choice != 0) {
        cout << "CAN'T DELETE MORE" << endl;
    }
}




void saveData() {
    json j;
    for (int i = 1; i < (int)TABLE.size(); i++) {
        j["useTable"][to_string(i)] = useTable[i];
        json tJ; tJ["count"] = TABLE[i].count; tJ["total"] = TABLE[i].total;
        for (int k = 0; k < TABLE[i].count; k++) {
            tJ["orders"].push_back({ {"item", TABLE[i].List[k]}, {"price", TABLE[i].Price[k]}, {"amount", TABLE[i].Amount[k]} });
        }
        j["tables"][to_string(i)] = tJ;
    }
    ofstream file("database.json"); file << j.dump(4);

}

void saveDataformanageinjson() {
    json j2;
    for (int i = 1; i < (int)TABLE.size(); i++) {
        j2["useTable"][to_string(i)] = useTable[i];
        json tJ2; tJ2["count"] = TABLE[i].count; tJ2["total"] = TABLE[i].total;
        for (int k = 0; k < TABLE[i].count; k++) {
            tJ2["orders"].push_back({ {"item", TABLE[i].List[k]}, {"price", TABLE[i].Price[k]}, {"amount", TABLE[i].Amount[k]} });
        }
        j2["tables"][to_string(i)] = tJ2;
    }
    ofstream file("alldatabaseinfo.json"); file << j2.dump(4);
}


void loadData() {
    ifstream file("database.json");
    if (!file.is_open()) { TABLE.resize(6); useTable.assign(6, 0); return; }
    json j; file >> j;
    int savedTableCount = j["tables"].size();
    TABLE.resize(savedTableCount + 1); useTable.resize(savedTableCount + 1);
    for (int i = 1; i < TABLE.size(); i++) {
        string s = to_string(i);
        useTable[i] = j["useTable"].value(s, 0);
        if (j["tables"].contains(s)) {
            TABLE[i].count = j["tables"][s].value("count", 0);
            TABLE[i].total = j["tables"][s].value("total", 0);
            for (auto& o : j["tables"][s]["orders"]) {
                TABLE[i].List.push_back(o.value("item", ""));
                TABLE[i].Price.push_back(o.value("price", 0));
                TABLE[i].Amount.push_back(o.value("amount", 0));
            }
        }
    }
}

void resetData() {
    int confirm;
    cout << "\n!!! WARNING: RESET ALL CURRENT DATA !!!" << endl;
    cout << "1. Confirm / 2. Cancel: ";
    cin >> confirm;

    if (confirm == 1) {
        // 1. เคลียร์ข้อมูลใน RAM
        for (int i = 0; i < TABLE.size(); i++) {
            TABLE[i].List.clear();
            TABLE[i].Price.clear();
            TABLE[i].Amount.clear();
            TABLE[i].count = 0;
            TABLE[i].total = 0;
        }
        fill(useTable.begin(), useTable.end(), 0);

        // 2. สั่ง Save เฉพาะ database.json (ไฟล์หลัก)
        saveData();

        cout << ">>> RESET COMPLETED: database.json has been cleared. <<<" << endl;
    }
    else {
        cout << ">>> RESET CANCELLED <<<" << endl;
    }
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
            saveDataformanageinjson();
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
