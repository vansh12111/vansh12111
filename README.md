print(" ----------------Welcome to Agarwal Bank---------------")
print("How can I help you")
import mysql.connector as a
con=a.connect(host='localhost',user="root",password='admin',database='agarwal_bank')
#Enter Details of New customer
def openAcc():
        n=input("Enter Your Account Name:")
        ac=int(input("Enter Your Account Number:"))
        bd=int(input("Enter your D.O.B:"))
        p=input("Enter Your Phone Number: +91")
        ad=input("Enter your adress:")
        adh=int(input("Enter your Aadhar Number:"))
        ID=input("Enter your Passport Id")
        ob=int(input("Enter your Openning Balance:"))
        g='insert into account(n,ac,bd,p,ad,adh,ID,ob)valuess(%s,%s,%s,%s,%s,%s,%s,%s,)'
        v='insert into amount(n,ac,ob) values (%s,%s,%s,)'
        c=con.cursor()
        c.execute(g, (n, ac, bd, p, ad, adh, ID, ob))
        c.execute(v, (n, ac, ob))
        con.commit(s)
        print("---------------Data Enetered Sucessfully-------------------")
        main()
#deposite the amount of existing customer
def depoAmo():
        am=int(input("Enter Amount: "))
        ac=int(input("Enter Your Account Name:"))
        a="select balance from amount where acno=%s"
        y=(ac,am)
        c=con.cursor
        c.execute(a,y)
        myresult=c.fethchone
        toam=myresult[0]+am
        sql="update amount set balance=%s where acno=%s"
        d=(toam,ac)
        c.execute (sql,d)
        con.commit()
        main()
#withdraw the amount of existing customer
def witham():
        am= int(input("Enter Amount :"))
        ac=int(input("Enter Account No"))
        a="select balance from amount where acno= %s"
        b=(ac,am)
        c=con.cursor()
        c.execute(a,b)
        myresult=c.fetchone()
        tam=myresult[0]-am
        z="update amount set balance=%s where acno=%s"
        x=(tam,ac)
        c.execute(z,x)
        con.commit()
        main()
def balance():
        ac=input("Enter Account No:")
        a="select balance from amount where acno=%s"
        k=(ac)
        c=con.cursor()
        c.execute(a,k)
        myresult=c.fetchone()
        print("Balance for Account:",ac,"is",myresult[0])
        main()
def dispacc():
        ac=input("Enter Account No: ")
        a="select*from account where acno = %s"
        l=(ac)
        c=con.cursor()
        c.execute(a,l)
        myresult=c.fetchone()
        for i in myresult:
                print(i,end=" ")
        main()
def closeac():
        ac=input("Enter Account No:")
        sql3="delete from account where acno=%s"
        sql4="delete from amount where acno=%s"
        j=(ac)
        c=con.cursor()
        c.execute(sql3,j)
        c.execute(sql4,j)
        con.commit()
        main()
def main():
    print("""
    1. OPEN NEW ACCOUNT
    2. DEPOSIT AMOUNT
    3. WITHDRAW AMOUNT
    4. BALANCE ENQUIRY
    5. DISPLAY CUSTOMERS DETAILS
    6. CLOSE AN ACCOUNT
    7. EXIT
    """)
    Choice = input("Enter Task No:")
    if Choice == "1":
        openAcc()
    elif Choice == "2":
        depoAmo()
    elif Choice == "3":
        witham()
    elif Choice == "4":
        balance()
    elif Choice == "5":
        dispacc()
    elif Choice == "6":
        closeac()
    elif Choice == "7":
        con.close()  # Close the database connection
        print("Goodbye!")
        exit()
    else:
        print("Wrong Choice...............")
        main()

main()

        
        
