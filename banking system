//Banking System using Structures and File Handling.
#include <stdio.h>
#include <stdlib.h>

struct Account
{
    int accNo;
    char name[50];
    float balance;
};

void createAccount();
void displayAccounts();
void depositMoney();
void withdrawMoney();

int main()
{
    int choice;

    while(1)
    {
        printf("\n===== BANKING SYSTEM =====\n");
        printf("1. Create Account\n");
        printf("2. Display Accounts\n");
        printf("3. Deposit Money\n");
        printf("4. Withdraw Money\n");
        printf("5. Exit\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch(choice)
        {
            case 1:
                createAccount();
                break;
            case 2:
                displayAccounts();
                break;
            case 3:
                depositMoney();
                break;
            case 4:
                withdrawMoney();
                break;
            case 5:
                printf("Thank You!\n");
                exit(0);
            default:
                printf("Invalid Choice!\n");
        }
    }

    return 0;
}

void createAccount()
{
    FILE *fp;
    struct Account a;

    fp = fopen("bank.dat", "ab");

    printf("Enter Account Number: ");
    scanf("%d", &a.accNo);

    printf("Enter Account Holder Name: ");
    scanf(" %[^\n]", a.name);

    printf("Enter Initial Balance: ");
    scanf("%f", &a.balance);

    fwrite(&a, sizeof(a), 1, fp);

    fclose(fp);

    printf("Account Created Successfully!\n");
}

void displayAccounts()
{
    FILE *fp;
    struct Account a;

    fp = fopen("bank.dat", "rb");

    if(fp == NULL)
    {
        printf("No Accounts Found!\n");
        return;
    }

    printf("\n----- Account Details -----\n");

    while(fread(&a, sizeof(a), 1, fp))
    {
        printf("Account No : %d\n", a.accNo);
        printf("Name       : %s\n", a.name);
        printf("Balance    : %.2f\n", a.balance);
        printf("----------------------------\n");
    }

    fclose(fp);
}

void depositMoney()
{
    FILE *fp;
    struct Account a;
    int acc, found = 0;
    float amount;

    fp = fopen("bank.dat", "rb+");

    if(fp == NULL)
    {
        printf("No Accounts Found!\n");
        return;
    }

    printf("Enter Account Number: ");
    scanf("%d", &acc);

    while(fread(&a, sizeof(a), 1, fp))
    {
        if(a.accNo == acc)
        {
            printf("Enter Amount to Deposit: ");
            scanf("%f", &amount);

            a.balance += amount;

            fseek(fp, -sizeof(a), SEEK_CUR);
            fwrite(&a, sizeof(a), 1, fp);

            printf("Deposit Successful!\n");
            printf("Updated Balance: %.2f\n", a.balance);

            found = 1;
            break;
        }
    }

    if(!found)
        printf("Account Not Found!\n");

    fclose(fp);
}

void withdrawMoney()
{
    FILE *fp;
    struct Account a;
    int acc, found = 0;
    float amount;

    fp = fopen("bank.dat", "rb+");

    if(fp == NULL)
    {
        printf("No Accounts Found!\n");
        return;
    }

    printf("Enter Account Number: ");
    scanf("%d", &acc);

    while(fread(&a, sizeof(a), 1, fp))
    {
        if(a.accNo == acc)
        {
            printf("Enter Amount to Withdraw: ");
            scanf("%f", &amount);

            if(amount > a.balance)
            {
                printf("Insufficient Balance!\n");
            }
            else
            {
                a.balance -= amount;

                fseek(fp, -sizeof(a), SEEK_CUR);
                fwrite(&a, sizeof(a), 1, fp);

                printf("Withdrawal Successful!\n");
                printf("Remaining Balance: %.2f\n", a.balance);
            }

            found = 1;
            break;
        }
    }

    if(!found)
        printf("Account Not Found!\n");

    fclose(fp);
}
