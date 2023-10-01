# bank-simulation-using-OOP
My program which simulates operations of an working bank.
import java.io.IOException;
import java.util.logging.Level;
import java.util.logging.Logger;
import java.util.Scanner;
import java.io.BufferedReader;
import java.io.InputStreamReader;
public class practise{
public static void main(String[] args)throws Exception{
BufferedReader bufferedReader=new BufferedReader(new
InputStreamReader(System.in));
int numberOfCustomers=0;
Bank bank=new Bank();
Customer[] c=bank.getCustomer();
while(true){
System.out.println("Please enter your choice:");
System.out.println("1.Add customer");
System.out.println("2.Deposit money");
System.out.println("3.Withdraw money");
System.out.println("4.Check balance");
System.out.println("5.Calculate interest");
System.out.println("6.Exit");
int choice=Integer.parseInt(bufferedReader.readLine());
switch(choice){
case 1:System.out.println("Creating an account for a new customer.");
System.out.println("Please enter the initial amount in your
account:");
double bal=Double.parseDouble(bufferedReader.readLine());
System.out.println("Please enter account number:");
String acc=bufferedReader.readLine();
Account account=new Account(bal, acc);
System.out.println("Please enter your name");
String name=bufferedReader.readLine();
Customer customer=new Customer(name,account);
c[numberOfCustomers]=customer;
numberOfCustomers++;
System.out.println("Customer count: "+numberOfCustomers);
for(int i=0;i<numberOfCustomers;i++){
System.out.println(c[i].getName()+"Name");
}
break;
case 2:System.out.println("Enter account number");
acc=bufferedReader.readLine();
if(numberOfCustomers==0){
System.out.println("Account number not found");
}
else{
boolean found=false;
for(int i=0;i<numberOfCustomers;i++){
Account temp=c[i].getAccount();
String accTemp=temp.getAccountNumber();
if(accTemp==acc){
System.out.println("Please enter the amount to deposit: ");
double
money=Double.parseDouble(bufferedReader.readLine());
temp.deposit(money);
found=true;
}
}
if(found==false){
System.out.println("Account number not found");
}
}
break;
case 3:System.out.println("Enter account number");
acc=bufferedReader.readLine();
if(numberOfCustomers==0){
System.out.println("Account number not found");
}
else{
boolean found=false;
for(int i=0;i<numberOfCustomers;i++){
Account temp=c[i].getAccount();
String accTemp=temp.getAccountNumber();
if(accTemp==acc){
System.out.println("Please enter the amount to withdraw: ");
double
money=Double.parseDouble(bufferedReader.readLine());
temp.withdraw(money);
found=true;
}
}
if(found==false){
System.out.println("Account number not found");
}
}
break;
case 4:System.out.println("Enter account number");
acc=bufferedReader.readLine();
if(numberOfCustomers==0){
System.out.println("Account number not found");
}
else{
boolean found=false;
for(int i=0;i<numberOfCustomers;i++){
Account temp=c[i].getAccount();
String accTemp=temp.getAccountNumber();
if(accTemp==acc){
System.out.println("Balance is: "+temp.getBalance());
found=true;
}
}
if(found==false){
System.out.println("Account number not found");
}
}
break;
case 5:System.out.println("Enter account number");
acc=bufferedReader.readLine();
if(numberOfCustomers==0){
System.out.println("Account number not found");
}
else{
boolean found=false;
for(int i=0;i<numberOfCustomers;i++){
Account temp=c[i].getAccount();
String accTemp=temp.getAccountNumber();
if(accTemp==acc){
bank.calculateInterest(c[i]);
found=true;
}
}
if(found==false){
System.out.println("Account number not found");
}
}
break;
case 6:System.exit(0);
default: break;
}
}
}
}
class Bank{
private double interestRate=8.5;
private double transactionFees=10;
private Customer[] customers=new Customer[1000];
public void calculateInterest(Customer customer){
Account a=customer.getAccount();
double bal=a.getBalance();
double interestAmount=bal*interestRate/100;
double totalBalance=bal=interestAmount;
System.out.println("Interest amount: "+interestAmount+" Total money after
adding interest: "+totalBalance);
}
public double getInterestRate(){
return interestRate;
}
public double getTransactionFees(){
return transactionFees;
}
public Customer[] getCustomer(){
return customers;
}
}
class Account{
private double balance=100;
private String accountNumber;
private boolean firstTime=true;
public Account(String acc){
accountNumber=acc;
}
public Account(double bal,String acc){
if(bal>=100){
balance=bal;
}
else{
balance=100;
}
accountNumber=acc;
}
public void deposit(double howMuch){
if(howMuch>0){
balance=balance+howMuch;
System.out.println("Amount successfully deposited."+"The new balance of
your account is"+ balance);
}
else{
System.out.println("Please ensure amount to be deposited is not
negative.");
}
}
public void withdraw(double howMuch){
if(howMuch>=0){
if(firstTime==true){
double tempBalance=balance;
tempBalance=tempBalance-howMuch;
if(tempBalance>=100){
balance=balance-howMuch;
}
else{
System.out.println("Insufficient balance to perform withdrawal.");
}
firstTime=false;
}
else{
Bank bank=new Bank();
double tempBalance=balance;
tempBalance=tempBalance-howMuch-bank.getTransactionFees();
if(tempBalance>=100){
balance=balance-howMuch-bank.getTransactionFees();
}
else{
System.out.println("Insufficient balance to perform withdrawal.");
}
}
}
else{
System.out.println("Please ensure the amount to be withdrawn is not
negative.");
}
}
public double getBalance(){
return balance;
}
public String getAccountNumber(){
return accountNumber;
}
}
class Customer{
private String name;
private Account account;
Customer(String n, Account a){
name=n;
account=a;
}
public void display(){
System.out.println("Name: "+name+", Account Number:
"+account.getAccountNumber()+", Balance: "+account.getBalance());
}
public String getName(){
return name;
}
public Account getAccount(){
return account;
}
}
