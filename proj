//Project 01

#include <iostream>
#include <ctime>
#include <vector>
#include <fstream>
using namespace std;

void runGame(int choice);
int randomRoll();
int roundSelection();
int makeChoice();
int getOutcome(int pInput, int cInput);
void outputRoundResult(int result,string name);
void printResults(vector<int> outcomes, string name);
void outputChoice(int roll);
bool winnerCheck(vector<int> outcomes);
bool checkIfGameOver(vector<int> outcomes,int rounds);
void printToFile(vector<int> outcomes, string name);


int main()
{
    bool valid=false;
    while(!valid){
        cout<<"Welcome to Rock, Paper, Scissors!\nChoose between these options:\n(1)Player vs. Computer\n(2)Computer vs. Computer\n(3)Exit"<<endl;
        int choice;
        cin>>choice;
        if(choice==3){
            valid=true;
            exit;
        }
        else if(choice==1 || choice==2){
            valid=true;
            runGame(choice);
        }
        else{
            cout<<"Please enter a valid choice."<<endl;
        }
    }
    return 0;
}

void runGame(int choice){
    string name;
    if(choice==1){
        cout<<"Please enter your name!"<<endl;
        cin>>name;
    }
    if(choice==2){
        name="Computer1";
    }
    int rounds = roundSelection();
    vector<int> roundOutcomes(0);
    //the round process
    for(int x=0;x<rounds;x++){
        if(checkIfGameOver(roundOutcomes,rounds)){
            break;
        }
        cout<<endl;
        int playerChoice=randomRoll();
        int computerChoice=randomRoll();
        if(choice==1){
            playerChoice=makeChoice();
            outputChoice(computerChoice);
        }
        int output=getOutcome(playerChoice,computerChoice);
        while(output==3){
            computerChoice=randomRoll();
            if(choice==1){
                cout<<"That was a draw, make a new selection."<<endl;
                playerChoice=makeChoice();
                outputChoice(computerChoice);
            }
            if(choice==2){
                playerChoice=randomRoll();
            }
            output=getOutcome(playerChoice,computerChoice);
        }
        outputRoundResult(output,name);
        roundOutcomes.push_back(output);
    }
    printResults(roundOutcomes,name);
    char yesOrNo;
    cout<<"Would you like to save these results to a file?(y/n)"<<endl;
    cin>>yesOrNo;
    if(yesOrNo=='n')
        cout<<"Thanks for playing!";
    if(yesOrNo=='y'){
        printToFile(roundOutcomes,name);
        cout<<"Thanks for playing!";
    }
}

int roundSelection(){//confirms the number of rounds that the user inputs are odd and positive
    bool valid=false;
    int input;
    while(!valid)
    {
        cout<<"Please enter the number of rounds you want to play! This must be an odd amount!"<<endl;
        cin>>input;
        if(((input%2)==1)&&(input>0)){
            valid=true;
        }
        else{
            cout<<"You did not enter an odd number. Try again."<<endl;
        }
    }
    return input;
}

int makeChoice(){//The player chooses a valid choice and the function returns the number corresponding to the choice
    bool valid=false;
    int choice;
    while(!valid){
        cout<<"Choose either:\n(1)Rock\n(2)Paper\n(3)Scissors"<<endl;
        cin>>choice;
        if(choice==1||choice==2||choice==3){
            valid=true;
        }
        else{
            cout<<"Invalid Choice."<<endl;
        }
    }
    return choice;
}

int getOutcome(int pInput, int cInput){//outcome of 1 means pInput wins, 2 means cInput wins, and 3 means draw
    if(pInput==cInput){
        return 3;
    }
    //Rock is 1, Paper is 2, Scissors is 3
    if(pInput==1&&cInput==2){
        return 2;
    }
    if(pInput==1&&cInput==3){
        return 1;
    }
    if(pInput==2&&cInput==3){
        return 2;
    }
    if(pInput==2&&cInput==1){
        return 1;
    }
    if(pInput==3&&cInput==1){
        return 2;
    }
    if(pInput==3&&cInput==2){
        return 1;
    }
    return 0;
}

int randomRoll(){ //Returns a random value from 1-3 signifying rock paper or scissors
    srand(time(0));
    int a=(rand()%3)+1;
    return a;
}


void outputRoundResult(int result,string name){//outputs the winner to the terminal
    if(result == 1){
        cout<<name<<" won the round!"<<endl;
    }
    else if(result == 2){
        cout<<"Computer won the round!"<<endl;
    }
}



void printResults(vector<int> outcomes, string name){//prints the results of the game
    cout<<"Here are the results of your game!"<<endl;
    cout<<"Round  |"<<name<<" | Computer"<<endl;
    cout<<"--------------------------------------------"<<endl;
    int roundnum=1;
    for(int x=0; x<outcomes.size();x++){
        cout<<roundnum;
        if(outcomes[x]==1){
            cout<<"      | W      | L      "<<endl;
        }
        else if(outcomes[x]==2){
            cout<<"      | L      | W      "<<endl;
        }
        roundnum++;
    }
    bool win=winnerCheck(outcomes);
    if(win){
        cout<<name<<" wins!"<<endl;
    }
    else{
        cout<<"Computer wins!"<<endl;
    }
}

void outputChoice(int roll){//outputs what the computer chose
    switch(roll){
        case 1:
        cout<<"Computer chose Rock. ";
        break;
        case 2:
        cout<<"Computer chose Paper. ";
        break;
        case 3:
        cout<<"Computer chose Scissors. ";
        break;
    }
}

bool winnerCheck(vector<int> outcomes){//returns true if player 1 wins, false if player 2 wins
    int winCount;
    int loseCount;
    for(int x=0;x<outcomes.size();x++){
        if(outcomes[x]==1)
            winCount++;
        if(outcomes[x]==2)
            loseCount++;
    }
    if(winCount>loseCount){
        return true;
    }
    return false;
    
}



bool checkIfGameOver(vector<int> outcomes,int rounds){//this function returns true if the game has been decided or false if the game has not been decided
    int winCount=0;
    int loseCount=0;
    for(int x=0;x<outcomes.size();x++){
        if(outcomes[x]==1)
            winCount++;
        if(outcomes[x]==2)
            loseCount++;
    }
    if((winCount>rounds/2)||(loseCount>rounds/2))
    {
        return true;
    }
    return false;
}


void printToFile(vector<int> outcomes, string name){//outputs the results to a text file
    time_t ttime = time(0);
    tm *local_time = localtime(&ttime);

    string filename = name+"_CPU"+"_Results_"+to_string(1 + (local_time->tm_mon))+"-"+to_string(local_time->tm_mday)+"-"+to_string(1900 + (local_time->tm_year))+"-"+to_string((local_time->tm_hour))+ ":" + to_string(1 + (local_time->tm_min)) ;
    
    ofstream outfile ((filename+".txt"));
    outfile<<"Here are the results of your game!"<<endl;
    outfile<<"Round  |"<<name<<" | Computer"<<endl;
    outfile<<"--------------------------------------------"<<endl;
    int roundnum=1;
    for(int x=0; x<outcomes.size();x++){
        outfile<<roundnum;
        if(outcomes[x]==1){
            outfile<<"      | W      | L      "<<endl;
        }
        else if(outcomes[x]==2){
            outfile<<"      | L      | W      "<<endl;
        }
        roundnum++;
    }
    bool win=winnerCheck(outcomes);
    if(win){
        outfile<<name<<" wins!"<<endl;
    }
    else{
        outfile<<"Computer wins!"<<endl;
    }
    outfile.close();
}








/*
/******************************************************************************
EXTRA CODE FOR TIME AND STUFF
*******************************************************************************/

#include <iostream>
#include <vector>
#include <ctime>
using namespace std;

int main()
{
	            time_t ttime = time(0);
                 cout << "Number of seconds elapsed since January 1, 1990:" << ttime << endl;
                 tm *local_time = localtime(&ttime);
    
                 cout << "Year: "<< 1900 + local_time->tm_year << endl;
                 cout << "Month: "<< 1 + local_time->tm_mon<< endl;
                 cout << "Day: "<< local_time->tm_mday << endl;
                 cout << "Time: "<< 1 + local_time->tm_hour << ":";
                 cout << 1 + local_time->tm_min << ":";
                 cout << 1 + local_time->tm_sec << endl;
    return 0;
}

*/

