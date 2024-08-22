   

Introduction to Active Directory

![e7f5c90fe654617c81cf3e1e1a97509e.png](e6cdd83ece0240419379aa906325ad3a.png)

Active Directory Structure  
![338b70d3ab67242e87ce8aa8c2c8c5e1.png](11560d26bd35462b8eae4d5621862338.png)  
![c85dfe3f584a628190e04e72f561d80a.png](356f40d78e294f778ddc8df133af5b6e.png)

- Forest -> Tree -> Domains -> nested subdomains -> OU (DC, Users, PC)

---

- Objects
- Attributes
- Schema
- Domain
- Forest
- Tree
- Container
- Leaf

FSMO roles

1. Schema Master (One of each per forest)
2. Domain Naming Master (One of each per forest)
3. Relative ID (RID) Master (One per domain)
4. Infrastructrue Master (One per domain)
5. Primary Domain Controller (PDC) Emulator (One per domain)