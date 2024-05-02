# HalloweenProject
/******************************************************************************
Author: Salim Tagemouati
Date-Written:11/7/23
Description: This program will ask for the name, gender, ager, costume name 
             arrival time, and rating. The program calculates number of pieces of candy.
             It keeps total for kids, gender, average rating, and total pieces of candy. 
             it calculates the rating for each costume.
*******************************************************************************/
#include <iostream>
#include <string>
#include <algorithm>
#include <iomanip>

using namespace std;

int main()
{
    // ****************************** PROGRAM VARIABLES ************************************

    string kid_nm[10]; // array for trick or treater name
    char sex_cd[10];    // Fixed the array size to 10
    string sex_nm[10];  // Fixed the array size to 10
    int age_no[10] = {0};
    int costume_cd[10] = {0};
    string costume_nm[5] = {"Disney", "Scary", "Super Hero", "Unknown", "None"};
    int hour_no[10] = {0};
    int minute_no[10] = {0};
    string rating_nm[5] = {"Top 10", "Top 25", "Top 100"};
    int rating_no[10] = {0};
    float avg_rating_no = 0; // Changed to a single float for average rating
    int candy_no[10] = {0};

    int tot_kids_no = 0;
    int tot_boys_no = 0;
    int tot_girls_no = 0;
    int tot_unknown_no = 0;
    float tot_age = 0;
    float tot_avg_age = 0;
    int tot_rating = 0;
    int tot_candy_no = 0;
    int i = 0;
    int j = 0;

    // ******************************** Get Input *****************************************

    cout << "Please enter the name of the Trick-or-Treater (Enter 'QUIT' to End Data Input): ";
    getline(cin, kid_nm[i]);
    transform(kid_nm[i].begin(), kid_nm[i].end(), kid_nm[i].begin(), ::toupper);

    while (kid_nm[i] != "QUIT")
    {
        cout << "Please enter " << kid_nm[i] << "'s gender (M, F, U): ";
        cin >> sex_cd[i];
        sex_cd[i] = toupper(sex_cd[i]);

        while (sex_cd[i] != 'M' && sex_cd[i] != 'F' && sex_cd[i] != 'U')
        {
            cout << " ********** ERROR ***************" << endl;
            cout << " Gender codes must be M (Male), F (Female) or U (Unknown)" << endl;
            cout << "You entered " << sex_cd[i] << endl;
            cout << "Please enter " << kid_nm[i] << "'s gender (M, F, U): ";
            cin >> sex_cd[i];
            sex_cd[i] = toupper(sex_cd[i]);
        }

        cin.clear();
        cin.ignore(100, '\n');

        cout << "Please enter " << kid_nm[i] << "'s age: ";
        cin >> age_no[i];

        cout << "**********************************" << endl;
        cout << "Please select the costume style: " << endl;
        cout << "**********************************" << endl;

        for (j = 0; j < 5; ++j)
        {
            cout << j + 1 << ". " << costume_nm[j] << endl;
        }

        cin >> costume_cd[i];

        while (costume_cd[i] < 1 || costume_cd[i] > 5)
        {
            cout << "************ ERROR **********************" << endl;
            cout << "Costume number must be 1 through 5" << endl;
            cout << "You entered " << costume_cd[i] << endl;
            cout << "Please enter " << kid_nm[i] << "'s costume code: ";
            cin >> costume_cd[i];
        }

        for (j = 0; j < 5; ++j)
        {
            cout << j + 1 << ". " << costume_nm[j] << endl;
        }

        cin >> costume_cd[i];

        --costume_cd[i]; // account for zero in the array list

        cout << "**********************************" << endl;
        cout << "Please select the Costume rating: " << endl;
        cout << "**********************************" << endl;

        for (j = 0; j < 3; ++j)
        {
            cout << j + 1 << "." << rating_nm[j] << endl;
        }

        cin >> rating_no[i];

        while (rating_no[i] < 1 || rating_no[i] > 3)
        {
            cout << "*************** ERROR  *********************" << endl;
            cout << "Costume rating must be 1 through 3 " << endl;
            cout << "You entered " << rating_no[i] << endl;
            cout << "Please enter " << kid_nm[i] << "'s costume rating: ";
            cin >> rating_no[i];
        }

        tot_rating += rating_no[i];

        cout << "Please enter the hour that " << kid_nm[i] << " showed up: ";
        cin >> hour_no[i];

        while (hour_no[i] < 1 || hour_no[i] > 12)
        {
            cout << " ********** ERROR ***************" << endl;
            cout << "Hour must be 1 through 12" << endl;
            cout << "You entered " << hour_no[i] << endl;
            cout << "Please enter " << kid_nm[i] << "'s hour: ";
            cin >> hour_no[i];
        }

        cout << "Please enter the minute that " << kid_nm[i] << " showed up: ";
        cin >> minute_no[i];

        while (minute_no[i] < 0 || minute_no[i] > 59)
        {
            cout << " ********** ERROR ***************" << endl;
            cout << "Minute must be 0 through 59" << endl;
            cout << "You entered " << minute_no[i] << endl;
            cout << "Please enter " << kid_nm[i] << "'s minute: ";
            cin >> minute_no[i];
        }

        ++tot_kids_no;

        switch (sex_cd[i])
        {
        case 'M':
            ++tot_boys_no;
            break;
        case 'F':
            ++tot_girls_no;
            break;
        case 'U':
            ++tot_unknown_no;
            break;
        }

        tot_age += age_no[i];

        if (age_no[i] < 10)
        {
            candy_no[i] = 2;
        }
        else
        {
            candy_no[i] = 1;
        }

        if (hour_no[i] < 5)
        {
            --candy_no[i];
        }

        if (hour_no[i] > 8)
        {
            ++candy_no[i];
        }

        ++i;

        cout << "Please Enter the name of the next Trick-or-Treater (Enter 'QUIT' to End Data Input): ";
        cin.ignore(); // Added to ignore newline character
        getline(cin, kid_nm[i]);
        transform(kid_nm[i].begin(), kid_nm[i].end(), kid_nm[i].begin(), ::toupper);
    }

    cout << setiosflags(ios::left);
    cout << "\t\t\t *****************************************************************************" << endl;
    cout << "\t\t\t *H A L L O W E E N   2 0 2 3   T R I C K - O R - T R E A T E R   R E P O R T*" << endl;
    cout << "\t\t\t *****************************************************************************" << endl;
    cout << setw(45) << "TRICK-OR-TREATER" << setw(15) << " COSTUME " << setw(15) << "TIME" << setw(15) << "COSTUME" << setw(15) << "PIECES" << endl;
    cout << setw(25) << "FIRST \t LAST " << setw(10) << " SEX" << setw(10) << "AGE" << setw(15) << "NAME" << setw(15) << "RATING" << endl;
    cout << setw(25) << "***** \t **** " << setw(10) << "***" << setw(10) << "***" << setw(15) << "****" << setw(15) << "*******" << endl;

    i = 0; // GO BACK TO THE TOP OF THE list
    while (kid_nm[i] != "QUIT")
    {
        cout << setw(25) << kid_nm[i] << setw(10) << sex_cd[i] << setw(10) << age_no[i]
             << setw(15) << costume_nm[costume_cd[i]] << setw(2) << hour_no[i]
             << ":" << setw(15) << minute_no[i] << setw(15) << rating_nm[rating_no[i]]
             << setw(10) << candy_no[i] << endl;
        ++i;
    }

    tot_avg_age = tot_age / tot_kids_no;
    float tot_avg_rating_no = static_cast<float>(tot_rating) / tot_kids_no;

    cout << "Total Kids: " << tot_kids_no << "\tTotal Boys: " << tot_boys_no << "\tTotal Girls: " << tot_girls_no << "\tTotal Unknown: " << tot_unknown_no << endl;
    cout << "Total Age: " << tot_age << "\tAverage Age: " << tot_avg_age << endl;
    cout << "Total Rating: " << tot_rating << "\tAverage Rating: " << tot_avg_rating_no << "\tTotal Candy: " << tot_candy_no << endl;

    return 0;
}
