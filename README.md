#include<iostream>
#include<fstream>
#include<string>
#include<cmath>
#include<iomanip>
#include<ctime>
using namespace std;
string filepath1="initial";
string filepath2="initial";
char menu_external(){
    char option_exter;
    cout<<endl<<endl<<endl<<endl;
    cout<<"                                            -----------------------------------------------------------------------        "<<endl<<endl;
    cout<<"                                                                       Login(Enter:L)"                                <<endl<<endl;
    cout<<"                                                              Openning current account (Enter:O)            "<<endl<<endl;
    cout<<"                                                                         Exit (Enter:E)"                                <<endl<<endl;
    cout<<"                                         Enter what you want to choose :"; cin>>option_exter; cout<<endl<<endl;
    cout<<"                                            -----------------------------------------------------------------------        "<<endl<<endl;
    return option_exter;
}
char menu_internal(){
    char option_inter;
    cout<<endl<<endl<<endl;
    cout<<"                                     --------------------------------------------------------------------------------------        "<<endl<<endl;
    cout<<"                                                                     Show Balance (Enter:B)"<<endl<<endl;
    cout<<"                                                                    Deposit Money (Enter : D)"<<endl<<endl;
    cout<<"                                           Share Account No.(Enter:Q)                        View Statment (Enter:V)"<<endl<<endl;
    cout<<"                                       Send Money (Enter:S)                                     Bills & Top up (Enter:K)"<<endl<<endl;
    cout<<"                                       Debit Card Apply (Enter:X)                                     Charity (Enter:C)"<<endl<<endl;
    cout<<"                                       Tax calculator(Enter:T)                                  Emi Culculator (Enter:L)"<<endl<<endl;
    cout<<"                                                                      Dicounts (Enter:I)"<<endl<<endl;
    cout<<"                                                                      Feedback (Enter:F)"<<endl<<endl;
    cout<<"                                                                      Change Password (Enter:P)"<<endl<<endl;
    cout<<"                                                                      Exit (Enter:E)"<<endl<<endl;
    cout<<"                                         Enter what you want to choose :"; cin>>option_inter; cout<<endl<<endl;
    cout<<"                                     --------------------------------------------------------------------------------------        "<<endl<<endl;
    return option_inter;
}
array<string, 2> login(){
    string username;
    string password;
    string line;
    string user_data[2];
    int count=0;
    ask:
    cout<<"Enter Your Username : ";
    cin>>username;
    cout<<endl;
    cin.ignore();
    cout<<"Enter your password : ";
    cin>>password;
    cout<<endl;
     fstream passw;
     passw.open("passwords_username.txt",ios::in);
     while(getline(passw,line)){
        if(username==line){
            count++;
        }
        if(password==line ){
            count++;
        }
     }
     passw.close();
    if(count<2){
        cout<<"Data is invalid .Enter correct Data"<<endl;
        goto ask;
    }
        if(count==2){
            array<string, 2> user_data = {username, password};
            return user_data;
        }
        
}
void account_opening_current(){
    string name;
    string cnic;
    int no_of_account=0;
    int account_no_start=111111;
    string password;
    string line;
    string username;
    int account_no;
    ask:
    cout<<"Enter Your Name : ";
    cin.ignore();
    getline(cin,name);
    cout<<"Enter your cnic no. : ";
    cin>>cnic;
    cout<<"Username should be of single word if with spaces the first will be considered but rest will be eliminated"<<endl<<endl;
    cout<<"Enter your Username : ";
    cin>>username;
    cout<<"Password should be of single word if with spaces the first will be considered but rest will be eliminated"<<endl<<endl;
    cout<<"Enter your Password : ";
    cin>>password;
    string check;
     fstream passw;
    passw.open("passwords_username.txt",ios::in);
    while(getline(passw,check)){
        if(check==username){
            passw.close();
            cout<<"\nUSERNAME ALREADY TAKEN PLEASE TRY ANOTHER ONE . <3"<<endl;
            goto ask;
        }
        if(check==username){
            passw.close();
            cout<<"\nPASSWORD ALREADY TAKEN PLEASE TRY ANOTHER ONE . <3"<<endl;
            goto ask;
        }
    }
    passw.close();
    if (name.empty() || cnic.empty() || password.empty()||username.empty()){
        cout<<"Invalid Data"<<endl;
        goto ask;
    }
    if (!name.empty() && !cnic.empty() && !password.empty() && !username.empty()){
    fstream info;
    info.open("information.txt",ios::out|ios::app);
    info<<name<<endl;
    info<<cnic<<endl;
    info.close();
    fstream opening;
    opening.open("accounts_no.txt",ios::in);
    while(getline(opening,line)){
        no_of_account++;
    }
    opening.close();
    opening.open("accounts_no.txt",ios::out | ios::app);
    account_no=(account_no_start+no_of_account);
    opening<<account_no<<endl;
    opening.close();
    cout<<"Your account no. is : "<<(account_no_start+no_of_account)<<endl;

     passw.open("passwords_username.txt",ios::out|ios::app);
    passw<<username<<endl;
    passw<<password<<endl;
    passw.close();
    }
    cout<<"Thanks for openning an account <3"<<endl;

}
void depositing(){
    int amount_depositing;
    string line;
    int count=0;
    cout<<"Enter The Amount That You Want to Deposit : ";
    cin>>amount_depositing;
    cout<<endl;
    fstream my_file1;
    my_file1.open(filepath1,ios::in);
             if(!my_file1.is_open()){
                cout<<"Failed to Open File "<<endl;
             }
             while(getline(my_file1,line)){
                count++;
             }
             if(count==0){
                line="0";
             }
             my_file1.close();
            amount_depositing=stoi(line)+amount_depositing;
            my_file1.open(filepath1,ios::out);
            my_file1<<amount_depositing;
             my_file1.close();
             time_t ct=time(0);
            string current_time= ctime(&ct);
             fstream my_file2;
             my_file2.open(filepath2,ios::app);
             my_file2<<"Amount Deposited : "<<amount_depositing<<"rps       Time : "<<current_time<<endl;
             my_file2.close();

             cout<<"Thanks For Depositing <3 "<<endl;

}
int withdraw(float withdrawal,string bill[][14],int company){
            string line;
            int balance;
             fstream my_file1;
             my_file1.open(filepath1 , ios::in);
             if(!my_file1.is_open()){
                cout<<"Failed to Open File "<<endl;
             }
            while(getline(my_file1,line)){
            }
            balance = stoi(line);
            if (withdrawal>balance){
                cout<<endl<< " INSUFFICIENT FUNDS "<<endl;
                return 0;
            }
             my_file1.close();
             my_file1.open(filepath1 , ios::out);
              if(!my_file1.is_open()){
                cout<<"Failed to Open File "<<endl;
             }
            balance = stoi(line);
            balance = balance - withdrawal;
            cin.ignore();
            my_file1<<balance;
             my_file1.close();
             time_t ct=time(0);
            string current_time= ctime(&ct);
             fstream my_file2;
             my_file2.open(filepath2,ios::app);
             my_file2<<"Amount Credited : "<<withdrawal<<"rps   "<<"Transfered To : "<<bill[0][company]<<"    Account no.  "<< bill[1][company]<<"   Time : "<<current_time<<endl;
             my_file2.close();
            cout<<endl<<"Transaction Successfully done .\n" << withdrawal <<" Rps has beed Debited from your Account . "<<endl;
            return 0;
}
int withdraw(int withdrawal,string s_account_num){
            string line;
            int balance;
             fstream my_file1;
             my_file1.open(filepath1 , ios::in);
             if(!my_file1.is_open()){
                cout<<"Failed to Open File "<<endl;
             }
            while(getline(my_file1,line)){
            }
            balance = stoi(line);
            if (withdrawal>balance){
                cout<<endl<< " INSUFFICIENT FUNDS "<<endl;
                return 0;
            }
             my_file1.close();
             my_file1.open(filepath1 , ios::out);
              if(!my_file1.is_open()){
                cout<<"Failed to Open File "<<endl;
             }
            balance = stoi(line);
            balance = balance - withdrawal;
            cin.ignore();
            my_file1<<balance;
             my_file1.close();
              time_t ct=time(0);
            string current_time= ctime(&ct);
             fstream my_file2;
             my_file2.open(filepath2,ios::app);
             my_file2<<"Amount Credited : "<<withdrawal<<"rps   "<<"Transfered To Account no. : "<<s_account_num<<"   Time : "<<current_time<<endl;
             my_file2.close();
            cout<<endl<<"Transaction Successfully done .\n" << withdrawal <<" Rps has beed Debited from your Account . "<<endl;
            return 0;
}
void bills_top_ups_payment(){
    int company;
    float payment;
    string bill[2][14]={{"LESCO", "IESCO", "FESCO", "GEPCO", "HESCO"," MEPCO", "PESCO", "QESCO"," SEPCO", "TESCO", "SNGPL", "SSGC", "PTCL"," WASA"},{"12345678901234", "23456789012345", "34567890123456", "45678901234567", "56789012345678", "67890123456789", "78901234567890", "89012345678901", "90123456789012", "01234567890123", "11234567890123", "21234567890123", "31234567890123", "41234567890123"}};
    ask:
    cout<<endl<<"LESCO (Lahore Electric Supply Company)        (Enter : 0) \nIESCO (Islamabad Electric Supply Company)        (Enter : 1) \n FESCO (Faisalabad Electric Supply Company)        (Enter : 2) \nGEPCO (Gujranwala Electric Power Company)        (Enter : 3) \nHESCO (Hyderabad Electric Supply Company)        (Enter : 4) \nMEPCO (Multan Electric Power Company)        (Enter : 5) \nPESCO (Peshawar Electric Supply Company)        (Enter : 6) \nQESCO (Quetta Electric Supply Company)        (Enter : 7) \nSEPCO (Sukkur Electric Power Company)        (Enter : 8) \nTESCO (Tribal Electric Supply Company)        (Enter : 9) \nSNGPL (Sui Northern Gas Pipelines Limited)        (Enter : 10) \nSSGC (Sui Southern Gas Company)        (Enter : 11)  \nPTCL (Pakistan Telecommunication Company Limited)        (Enter : 12) \nWASA (Water and Sanitation Agency)        (Enter : 13) "<<endl<<endl;
    cout<<"Enter a number for any selection of options : ";
    cin>>company;
    cout<<endl<<"Enter the amount you want to pay : ";
    cin>>payment;
    if(company<=14 && company>=0){
        withdraw(payment,bill,company);
    }
    else{
        cout<<"OPTION SELECTECTED IS INVALID .PLEASE TRY AGAIN \n";
        goto ask;
    }

}
void account_past_transaction(){
    int count;
    string line;
    fstream my_file1;
    my_file1.open(filepath2,ios::in);
    while(my_file1){
        getline(my_file1,line);
        cout<<line<<endl;
        count++;
    }
    my_file1.close();
    if(count==0){
        cout<<"NO TRANSACTIONS HAVE BEEN MADE TILL NOW <3";
    }
}
void show_balance(){
    string line;
    int count=0;
    cout<<"Your Current Balance is : ";
    fstream my_file1;
     my_file1.open(filepath1,ios::in);
            while(getline(my_file1,line)){
                count++;
            }
            if(count==0){
                line='0';
            }
            cout<<line;
             my_file1.close();
             cout<<endl<<endl;
}
void password_change(){
    string previous_password;
    string new_password;
    string password_update="";
    string line;
    int count=0;
    ask:
        cout<<endl<<"FOR CHANGING YOUR PASSWORD PLEASE RE-ENTER YOUR PREVIOUS PASSWORD : ";
        cin>>previous_password;
        cout<<endl;
        cout<<"ENTER YOUR NEW PASSWORD : ";
        cin>>new_password;
        fstream passw;
        passw.open("passwords_username.txt",ios::in);
        while(getline(passw,line)){
            if(line==previous_password){
                cin.ignore();
                line=new_password;
                count++;
            }
            password_update=password_update+line+"\n";
        }
        passw.close();
        cout<<password_update;
        passw.open("passwords_username.txt",ios::out);
        if(!passw){
            cout<<"\nUNABLE TO OPEN FILE\n";
        }
        passw<<password_update;
        passw.close();
        if(count>0){
        cout<<"\nPASSWORD CHANGED SUCCESSFULLY.\nTHANKS FOR PATIENCE.<3\n";
        }
        if(count==0){
        cout<<"\nTHE PASSWORD YOU HAVE ENETERED IS INCORRECT PLEASE TRY AGAIN .\n";
        goto ask;
        }


}
void zakat(){
    string account="BANK ZAKAT ACCOUNT";
    cout<<endl<<"FOR ZAKAT 2.5 PERCENT AMOUNT FROM YOUR MONEY IS BEING DEDUCTED ."<<endl;
    string line;
            int balance;
             fstream my_file1;
             my_file1.open(filepath1 , ios::in);
             if(!my_file1.is_open()){
                cout<<"Failed to Open File "<<endl;
             }
            while(getline(my_file1,line)){
            }
            balance = stoi(line); 
            my_file1.close();
            balance=2.5*balance/100;
            withdraw(balance,account);

}
void sadkat(){
    int company;
    float payment;
    string bill[2][14]={{"Edhi Foundation", "Shaukat Khanum Memorial Cancer Hospital", "Saylani Welfare International Trust", "Akhuwat Foundation", "Indus Hospital", "The Citizens Foundation (TCF)", "JDC Foundation Pakistan", "Transparent Hands", "Chhipa Welfare Association"},{"0014-7900-0013-01", "01-1423496-01", "0110-0101-6560-3303", "2010-0158-6180-001", "0017-7903-0013-02", "0012-0002-0030-24", "0564-0011-0058-8803", "0185-0101-1962-2903", "0012-1111-0015-03"}};
    ask:
    cout<<endl<<"Edhi Foundation       (Enter : 0)\n Shaukat Khanum Memorial Cancer Hospital     (Enter : 1)\n Saylani Welfare International Trust      (Enter : 2)\n Akhuwat Foundation      (Enter : 3)\n Indus Hospital      (Enter : 4)\n The Citizens Foundation (TCF)      (Enter : 5)\n JDC Foundation Pakistan      (Enter : 6)\n Transparent Hands      (Enter : 7)\n Chhipa Welfare Association      (Enter : 8)\n Agha Khan Development Network (AKDN)      (Enter : 9)"<<endl;
    cout<<"Enter Option you want to choose : ";
    cin>>company;
    cout<<endl<<"Enter the amount you want to give as sadkat: ";
    cin>>payment;
    if(company<=9 && company>=0){
        withdraw(payment,bill,company);
    }
    else{
        cout<<"OPTION SELECTECTED IS INVALID .PLEASE TRY AGAIN \n";
        goto ask;
    }

}
void charity(){
    char option;
    ask:
    cout<<endl<<"FOR ZAKAT (ENTER : Z)              FOR SADKAT (ENTER : S)"<<endl;
    cout<<"Enter : ";
    cin>>option;
    if(option=='Z'){
        zakat();
    }
    else if(option=='S'){
        sadkat();
    }
    else{
        cout<<endl<<"INVALID ENTRY . PLEASE TRY AGAIN <3"<<endl;
        goto ask;
    }

}
void discounts(){
    char city;
    char catagory;
    string line;
    cout<<"Lahore (Enter L)            Karachi(Enter K)            Isalamabad(Enter I)"<<endl;
    cout<<endl<<"Enter which city You want to choose : ";
    cin>>city;
    cout<<endl;
    switch(city){
        case 'L' :{
    cout<<"\nLife style (Enter L)        Health Care (Enter C)                 Food (Enter F)"<<endl;
    cout<<endl<<"Enter which catagory You want to choose :";
    cin>>catagory;
            switch(catagory){
        case 'L' :{
            fstream lifel;
            lifel.open("llifestyle.txt",ios::app);
            if(!lifel.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
                lifel.close();
            lifel.open("llifestyle.txt",ios::in);
            while(getline(lifel,line)){
                cout<<line<<endl;
            }
            lifel.close();
            break;
        }
        case 'C' :{
            fstream carel;
            carel.open("carel.txt",ios::app);
            if(!carel.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
                carel.close();
            carel.open("carel.txt",ios::in);
            while(getline(carel,line)){
                cout<<line<<endl;
            }
            carel.close();
            break;
        }
        case 'F' :{
            fstream foodl;
            foodl.open("foodl.txt",ios::app);
            if(!foodl.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
                foodl.close();
            foodl.open("foodl.txt",ios::in);
            while(getline(foodl,line)){
                cout<<line<<endl;
            }
            foodl.close();
            break;
        }
    }
            break;
        }
        case 'K' :{
        cout<<"\nLife style (Enter L)        Health Care (Enter C)                 Food (Enter F)"<<endl;
    cout<<endl<<"Enter which catagory You want to choose :";
    cin>>catagory;
            switch(catagory){
        case 'L' :{
            fstream lifek;
            lifek.open("klifestyle.txt",ios::app);
            if(!lifek.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
                lifek.close();
            lifek.open("klifestyle.txt",ios::in);
            if(!lifek.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
            while(getline(lifek,line)){
                cout<<line<<endl;
            }
            lifek.close();
            break;
        }
        case 'C' :{
            fstream carek;
            carek.open("carek.txt",ios::app);
            if(!carek.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
                carek.close();
            carek.open("carek.txt",ios::in);
            while(getline(carek,line)){
                cout<<line<<endl;
            }
            carek.close();
            break;
        }
        case 'F' :{
            fstream foodk;
            foodk.open("foodk.txt",ios::app);
            if(!foodk.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
                foodk.close();
            foodk.open("foodk.txt",ios::in);
            while(getline(foodk,line)){
                cout<<line<<endl;
            }
            foodk.close();
            break;
        }
    }
            break;
        }
        case 'I' :{
         cout<<"\nLife style (Enter L)        Health Care (Enter C)                 Food (Enter F)"<<endl;
    cout<<endl<<"Enter which catagory You want to choose :";
    cin>>catagory;
            switch(catagory){
        case 'L' :{
            fstream lifeI;
            lifeI.open("Ilifestyle.txt",ios::app);
            if(!lifeI.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
                lifeI.close();
            lifeI.open("Ilifestyle.txt",ios::in);
            if(!lifeI.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
            while(getline(lifeI,line)){
                cout<<line<<endl;
            }
            lifeI.close();
            break;
        }
        case 'C' :{
            fstream careI;
            careI.open("careI.txt",ios::app);
            if(!careI.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
            careI.close();
            careI.open("careI.txt",ios::in);
            while(getline(careI,line)){
                cout<<line<<endl;
            }
            careI.close();
            break;
        }
        case 'F' :{
            fstream foodI;
            foodI.open("foodI.txt",ios::app);
            if(!foodI.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
            foodI.close();
            foodI.open("foodI.txt",ios::in);
            while(getline(foodI,line)){
                cout<<line<<endl;
            }
            foodI.close();
            break;
        }
    }
            break;
        }
    }
}
void share_account_number(){
    
}
void apply_for_debit_card(string userdata[2]){
    string bill [2][14]={{"Bank"},{"Debit card charges"}};
        cout<<endl<<"Charges To Apply For Debit card are 500 rps.\n";
        fstream my_file1;
        my_file1.open("debit_card_apply.txt",ios::app);
        my_file1<<"USERNAME = "<<userdata[0]<<endl;
        my_file1.close();
        withdraw(500,bill,0);
        cout<<endl<<"THANKS FOR APPLYING FOR DEBIT CARD.\nREALLY APPRECIATE THAT. <3."<<endl;
        
        
}
void tax_calculator(){
    int income;
    float tax;
    char continu;
    do{
    cout<<"Enter your Yearly income in pkr : ";
    cin>>income;
    cout<<endl;
    cout<<fixed<<setprecision(3);
    if(income>0 &&income<=600000){
        cout<<"You are exempted from tax system and have to pay no taxes ."<<endl;
    }
    else if(income>600000 &&income<=1200000){
        tax=(5*income)/100;
        cout<<"You will have to pay 5% Tax on your income which is : "<<tax<<" pkr."<<endl;
    }
    else if(income>1200000 &&income<=2200000){
        tax=(15*income)/100;
        cout<<"You will have to pay 15% Tax on your income which is : "<<tax<<" pkr."<<endl;
    }
    else if(income>2200000 &&income<=3200000){
        tax=(25*income)/100;
        cout<<"You will have to pay 25% Tax on your income which is : "<<tax<<" pkr."<<endl;
    }
    else if(income>3200000 &&income<=4100000){
        tax=(30*income)/100;
        cout<<"You will have to pay 30% Tax on your income which is : "<<tax<<" pkr."<<endl;
    }
    else if(income>4100000){
        tax=(35*income)/100;
        cout<<"You will have to pay 35% Tax on your income which is : "<<tax<<" pkr."<<endl;
    }
    else{
        cout<<"Data you gave is incorrect";
    }
    ask:
     cout<<"Do you want to perform further calculation (For Yes Enter Y For Exit enter N) : ";cin>>continu;
     if(continu =='N' || continu=='Y'){
        goto loop;
     }
     if(continu !='N' || continu!='Y'){
        cout<<"Enter a valid entry ! "<<endl;
        goto ask;
     }
     loop:;
    }while(continu=='Y');
}
void emi_calculator(){
float loan,years;
float intrest;
float total_amount_paid;
float total_intrest;
char loan_type;
float emi;
char continu;
do{
cout<<"Enter the total loan that you want : "; cin>>loan; cout<<endl;
cout<<"For how many years you are getting it : "; cin>>years; cout<<endl;
cout<<"At what intrest rate are you getting it : ";cin>>intrest;
cout<<"If EMI is on flat intrest (Enter F) and if on Reducing balance (Enter R) : ";cin>>loan_type; cout<<endl;
cout<<fixed<<setprecision(3);
switch(loan_type){
    case 'F':{
        total_intrest=loan*intrest*years;
        emi=(loan+total_intrest)/(years*12);
        total_amount_paid=emi*years*12;
        cout<<"Total amount that you have to pay during the overal tenure is : "<<total_amount_paid<<" pkr."<<endl;
        cout<<"Total intrest that you have to pay during the overal tenure is : "<<total_intrest<<" pkr."<<endl;
        cout<<"Your monthly EMI is going to be : "<<emi<<" pkr."<<endl;
        break;
    }
    case 'R':{
         emi = (loan * intrest * pow(1 + intrest, years * 12)) / (pow(1 + intrest, years * 12) - 1);
        total_amount_paid=emi*years*12;
        total_intrest=total_amount_paid-loan;
         cout<<"Total amount that you have to pay during the overal tenure is : "<<total_amount_paid<<" pkr."<<endl;
        cout<<"Total intrest that you have to pay during the overal tenure is : "<<total_intrest<<" pkr."<<endl;
        cout<<"Your monthly EMI is going to be : "<<emi<<" pkr."<<endl;
        break;
    }
        }       
    ask:
    cout<<"Do you want to perform further calculation (For Yes Enter Y For Exit enter N) : ";cin>>continu;
    if(continu =='N' || continu=='Y'){
        goto loop;
     }
     if(continu !='N' || continu!='Y'){
        cout<<"Enter a valid entry ! "<<endl;
        goto ask;
     }
     loop:;
}while(continu=='Y');
    return;
    }
void feedback(string userdata[2]){
    string line;
        cout<<endl<<"ENTER FEEDBACK : ";
        cin.ignore();
        getline(cin,line);
        fstream my_file1;
        my_file1.open("feedback.txt",ios::app);
        my_file1<<"USERNAME = "<<userdata[0]<<"       FEEDBACK : "<<line<<endl;
        my_file1.close();
        cout<<endl<<"THANKS FOR YOUR FEEDBACK.\nREALLY APPRECIATE THAT. <3."<<endl;
}

int main(){
    bool  close_external=true;
    array<string, 2> user_data;
    do{
        char option_external;
        option_external = menu_external();
        switch (option_external)
        {
        case 'L':{
             user_data=login();
             filepath1=(user_data[0] +"_current_Balance.txt");
             fstream my_file1;
             my_file1.open(filepath1,ios::app);
             if(!my_file1.is_open()){
                cout<<"Failed to Open File "<<endl;
             }
             my_file1.close();
             filepath2=(user_data[0] +"_balance_History.txt");
             fstream my_file2;
             my_file2.open(filepath2,ios::app);
             if(!my_file2.is_open()){
                cout<<"Failed to Open File "<<endl;
             }
             my_file2.close();

            close_external=false;
            break;
        }
        case 'O':{
            account_opening_current();
            break;
        }
        case 'E':{
            return 0;
        }   
    }
    }while(close_external==true);
    char options_internal;
    bool closeinternal=true;
    string userdata[2];
    userdata[0]=user_data[0];
    userdata[1]=user_data[1];
    while(closeinternal==true){
        options_internal=menu_internal();
        switch (options_internal)
        {
        case 'D' :{
                depositing();
                break;
            }
        case 'S' :{
            int withdrawal ;
            string  s_account_num;
            cout<<"Enter The amount that you want to Send : ";
            cin>>withdrawal;
            cout<<endl;
            cout<<"Enter Account Number You Want to Send Money To : ";
            cin>>s_account_num;
            withdraw(withdrawal,s_account_num);
            break;
        }
        case 'B':{
            show_balance();
        }
         case 'Q':{
                share_account_number();
                break;
            }
         case 'V':{
                account_past_transaction();
                break;
            }
            case 'K':{
                bills_top_ups_payment();
                break;
            }
            case 'C':{
                charity();
                break;
            }

        case 'T':{
            tax_calculator();
            break;
        }
        case 'L':{
            emi_calculator();
            break;
        }
        case 'I':{
            discounts();
            break;
        }
        case 'X':{
            apply_for_debit_card(userdata);
            break;
        }
        case 'F':{
            feedback(userdata);
            break;
        }
        case 'P':{
            password_change();
            break;
        }
        case 'E':{
        closeinternal=false;
        break;
        }
    }
    }
    return 0;
    }
