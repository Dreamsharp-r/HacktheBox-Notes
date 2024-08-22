   

SQL Injection Fundamentals

NOTE: SQL injections refers to attacks against relational databases such as MySQL. whereas NoSQL injections refer to non-relational databases attacks.

![2a64a0156798ae8d34d7b99b5c5a879b.png](052f8296621342c18c6e3c0646303fa9.png)

![e39b202627df030f86969713c552734d.png](1e18a4472bfa4648b764faf88f1348bc.png)

- A SQL injection occurs when a malicious user attempts to pass input that changes the final SQL query sent by the web application to the database, enabling the user to perform other unintended SQL queries directly against the database.

Example of a SQL Injection  
![1cc7b1f42a1db282f6eda09ea1bb3f6f.png](2ce796cca18a4bc695be86cf88531127.png)

- Injecting a single quote (') can show whether a page is vulnerable.  
    ![612ee6fd57e743abfcd29c48e7ae0849.png](d4b95067270d42168790d1c1ad7834ad.png)

SQL Injection (AUTH BYPASS)  
![ad6d814b9c122370f2967a3f6e1b86fc.png](3257fa0e20c146d0a112fdf8a970b06e.png)  
![b480e00efc439a3a7d378ead96e05e57.png](e132f8afe0e0433fb3f89a243a21fc43.png)

TIP  
![793d79a4f9c9db0d1a1804c0f5338c23.png](dbed7b49ca984356bc4ad0bbd16788ad.png)  
![58cf8df978a6ac118fc0e888d2819978.png](4b8dbf71f38e4bce91461971847de483.png)

- Also use #
- In the URL # = %23

---

Union Injection  
![bf52835c13ceab205281d24f31f91ba6.png](0e45637b67cc4841a24704f925b54561.png)  
![36c37d2bf1b6488b0d4f1860725beb2a.png](1e456841e5c24dfbb3077edcebde14de.png)

- Very common that not every column will be displayed back to the user
- In this example column 1 is the ID field

---

DB Enumeration  
![d939ee70b415486c3d7a56a83eabcfad.png](30af6672ed4343a89143011012cddc9f.png)  
![608fafcd3190509b94d1f3ca5b6aefea.png](c915e18125e941cfbefec8d5f1eb73f4.png)

- To reference a table present in another DB use:  
    ![cb2adc42c6a3f8902e9b8620a0b7c1dc.png](952378a6b3304cc59898bd388bdec131.png)  
    Database -> Tables -> Columns -> Data

---

Privileges  
![03f67d87e2a1285033bdcfd758ee05a7.png](4a136e66edcc42c0854c2cb1b866f205.png)

- The Command below can also be used to find the current user  
    ![eac99e86468c87bfb3d17702a3d8254c.png](e1b46d11a1824213949aaab482407e82.png)  
    Use these command if within the DB  
    ![3ee6933ab84935b422def749dce98310.png](46751843760f4161be1212df37fb7432.png)
- Finds the current user  
    ![3657889311f6104365b2eae7204ed062.png](a0b4d07213b347b2b2446a142521bed8.png)
- Find if user has super admin privileges

---

File Injection  
![a2bb5ca723657d389e0d876234012ae8.png](1e88b3b4c310471f9708d2772736ab01.png)  
![8f1cb9daaf829b964e04058b711cc6c6.png](f16065ef57794d4ea6ff7787961d78cf.png)  
![7ceeba8834fcd2acf99fe86df10c8b14.png](a0c0071fe59e437f90ed36ad97d0ddfd.png)

- Look at Privilege Command "Find which directories can be accessed through MySQL"

![46bb58c1599acd48e77615271a97a159.png](a1c071acceb3476f86f070a724c04cc8.png)

- This request is injected into the php system
- Replace the command to enumerate the system

---

Command line  
![4a3a6459d4c3f16745c7713f42976cd6.png](979cc220491f452282569871df21b4e2.png)

- To specify a host use the:
    - -h and -p to specify ip and port

Commands  
![45584301df403a8145c42d8b8e48c67e.png](50941d4b6f5249d582df3c475256dc48.png)

![bc7c51fc802cac4b0e49efa0b2149f85.png](b76afde5152947e39279bb1531053bdd.png)

![877cb868106455736aa2024983970956.png](e9240b49c94f4a229555ff6bf2e17c52.png)

![1aa5f1fc1369f6b802ffbf1893ec2505.png](1028f84fe88b4b418598fa4a7150e19b.png)

Multiple Operator Precedence  
![befc19cfee95f3b88fb0bd324bf9be4f.png](0d268706b66a45769ae4688f4093a6dd.png)

Examples:  
![ab0de84bc1d8fca7170d76ab4d78d8ef.png](0eb5fcb1b4e54c1c8ed8aba031df7d3d.png)  
![6a76dc6aed91c32eb7fc7848ed83823a.png](8331478d0b724eb59007cec4bfd001c8.png)

- SHOW TABLES; //shows the table created
- DESCRIBE {table_name}; // show the table structure

![61a56569acb8288ce02016526d15a5e8.png](5ec6abe9cdc949038aecbf7a4c26f7f8.png)

- NOT NULL ensures that a particular column is never left empty. "i.e. required field"  
    ![11b70c7235267a1746e3a61806f51786.png](0ea8cb55717c49c99377ec2571920b60.png)
- UNIQUE ensures the inserted item is always unique  
    ![54ab61a97f54f4417184e00b827644d9.png](033113d2a8a74628b95b640e24d255d1.png)
- DEFAULT specify the default value within a column
- NOW() set the value to the current date and time  
    ![505a5651c3f41a136cea677610f26a44.png](f5a7a1b0ccda44528b7b6a594ba74582.png)
- PRIMARY KEY set the data of a record to be relational  
    ![e7dc296ce13a20a3cd2f186b151810b5.png](e15ae0cf61ac40c9b4a5ce03728cb47d.png)

Inserting values into Table  
![91fb763d61b6f6f811b3cfe1dbbc8e7c.png](58751ccffebd4858901015acb628c41e.png)

- Syntax above requires everything filled out  
    ![b1134450e43bd5ac1188298a4e6efcda.png](9d055e1b13dd4dda914891e7181581dc.png)
- With this syntax you can skip the id & date_of_joining
- Password should always be hashed/encrypted before storage  
    ![34c5d3890864bf0a5b83bc4d5a2a7846.png](68f350867d444c15bf4e193ad37e85cf.png)

Selecting Data from a Table to View  
![ce8497a883296b0d171f88ac7ef1eab9.png](b531bcb6e16043b6904c4007173628c8.png)

- - is a wild card and selects all columns
- View either tables or columns

Deleting Data from Database  
![90f15c1c1a01991efd2424d69cc5f7ab.png](a0d2758f826245fd8171185d97ce02b6.png)

Changing the Name, fields, or adding a column  
![f51d2147214570d3f08fdbcee5ab6da2.png](2d4e6d66357a45f4b0ebef768d85287e.png)

Updating information in a Table  
![eb08e5450fe895037f7fcdf4e72bc5c8.png](7a46d3be9ef4470196047cb2e7f4fdeb.png)  
![a2109a114507875e13660608da15bf84.png](610dd08ee071444eb87cd16cbbf64365.png)

Sorting Results  
![179a642ddf28a5187b88d5f65cce1a7d.png](3d7b26d356fc40a7a63795fab19d776b.png)  
![7aa3a78ea7415ce1765f018c760fcaa5.png](c398e2eff3cc4e8ab216574ce986b2f5.png)

Limiting the Result  
![50af965680e9a63fb9266adcd06abeb7.png](7aeda2136340480586e3815c02e72860.png)

Filtering the Data  
![fc0d2ebeaf22b45c25332cd909122e64.png](20dad8d2f8b14485b476c900de19aa24.png)  
![728e80a6bc66076161a296248162344a.png](5f72a4afe2c745d88c65d9068abc74dd.png)

Matching the Data to a Certain Pattern  
![e0e0127298ae7442b850acee7c24498b.png](0c4258e67d204655bd15d3cdc90b3dae.png)