#include<iostream>
#include<fstream>
#include<string>
#include<cmath>
#include<iomanip>
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
    cout<<"                                       Debit Card (Enter:X)                                     Zakat & Sadkat (Enter:Z)"<<endl<<endl;
    cout<<"                                       Tax calculator(Enter:T)                                  Emi Culculator (Enter:L)"<<endl<<endl;
    cout<<"                                                                      Dicounts (Enter:I)"<<endl<<endl;
    cout<<"                                                                      Feedback (Enter:F)"<<endl<<endl;
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
     fstream passw;
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
             cout<<"Thanks For Depositing <3 "<<endl;

}
int withdraw(int withdrawal,int s_account_num){
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
            cout<<endl<<"Transaction Successfully done ." << withdrawal <<" Rps has beed Debited from your Account . "<<endl;
            return 0;
}
void bills_top_ups_payment(){

}
void account_past_transaction(){

}
void addFeedback(string userdata[]){
    string feedback;
    fstream feed;
    feed.open("feedback.txt",ios::app);
    if(feed.is_open())
    {
        cout<<"Enter your feedaback:"<<endl;
        cin.ignore();
        getline(cin,feedback);
        feed<<"Feedback:"<<feedback<<endl;
        feed.close();
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

}
void zakat_and_sadqat(){

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
    cout<<"\nLife style (Enter L)        Health Care (Enter C)                 Food (Enter )"<<endl;
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
            carel.open("lcare.txt",ios::out);
            if(!carel.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
                carel.close();
            carel.open("lcare.txt",ios::in);
            while(getline(carel,line)){
                cout<<line;
            }
            carel.close();
            break;
        }
        case 'F' :{
            fstream foodl;
            foodl.open("foodl.txt",ios::out);
            if(!foodl.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
                foodl.close();
            foodl.open("foodl.txt",ios::in);
            while(getline(foodl,line)){
                cout<<line;
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
            lifek.open("klifestyle.txt",ios::out);
            if(!lifek.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
                lifek.close();
            lifek.open("klifestyle.txt",ios::in);
            if(!lifek.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
            while(getline(lifek,line)){
                cout<<line;
            }
            lifek.close();
            break;
        }
        case 'C' :{
            fstream carek;
            carek.open("carek.txt",ios::out);
            if(!carek.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
                carek.close();
            carek.open("carek.txt",ios::in);
            while(getline(carek,line)){
                cout<<line;
            }
            carek.close();
            break;
        }
        case 'F' :{
            fstream foodk;
            foodk.open("foodk.txt",ios::out);
            if(!foodk.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
                foodk.close();
            foodk.open("foodk.txt",ios::in);
            while(getline(foodk,line)){
                cout<<line;
            }
            foodk.close();
            break;
        }
    }
            break;
        }
        case 'I' :{
         cout<<"\nLife style (Enter L)        Health Care (Enter C)                 Food (Enter F)"<<endl;
         cout<<"          Student Discount(Enter S)           Happy Hour Discount(Enter H)"<<endl;
    cout<<endl<<"Enter which catagory You want to choose :";
    cin>>catagory;
            switch(catagory){
        case 'L' :{
            fstream lifeI;
            lifeI.open("Ilifestyle.txt",ios::out);
            if(!lifeI.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
                lifeI.close();
            lifeI.open("Ilifestyle.txt",ios::in);
            if(!lifeI.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
            while(getline(lifeI,line)){
                cout<<line;
            }
            lifeI.close();
            break;
        }
        case 'C' :{
            fstream careI;
            careI.open("careI.txt",ios::out);
            if(!careI.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
            careI.close();
            careI.open("careI.txt",ios::in);
            while(getline(careI,line)){
                cout<<line;
            }
            careI.close();
            break;
        }
        case 'F' :{
            fstream foodI;
            foodI.open("food_Isl.txt",ios::out);
            if(!foodI.is_open()){
                cout<<"Failed to Open File "<<endl;
                }
            foodI.close();
            foodI.open("foodI.txt",ios::in);
            while(getline(foodI,line)){
                cout<<line;
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
void apply_for_debit_card(){

}
void apply_for_credit_card(){

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
        emi=(loan*(intrest/12)*pow(1+(intrest/12),years*12))/pow(1+intrest/12,(years*12)-1);
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

void apply_for_loan(){

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
             my_file1.open(filepath1,ios::out);
             if(!my_file1.is_open()){
                cout<<"Failed to Open File "<<endl;
             }
             my_file1.close();
             filepath2=(user_data[0] +"_balance_History.txt");
             fstream my_file2;
             my_file2.open(filepath2,ios::out);
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
            int withdrawal ,s_account_num;
            cout<<"Enter The amount that you want to Send : ";
            cin>>withdrawal;
            cout<<endl;
            cout<<"Enter 11 digits Account Number : ";
            cin>>s_account_num;

            withdraw(withdrawal,s_account_num);
            break;
        }
        case 'B':{
            show_balance();
            break;
        }
         case 'Q':{
                share_account_number();
                break;
            }
         case 'V':{
                account_past_transaction();
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
        case 'F':{
        addFeedback(userdata);
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
