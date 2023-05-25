bases da orientação a objetos

=============================

dados + comportamento

// dados
user.c

const int typeAdmin = 0;
const int typeGuest = 1;
const int typeCustomer = 2;

struct user {
    int id;
    char[] name;
    int type;
    int role;
    int permission;
    *add;
}

//comportamento
user_management.c
free function:
function save(*user us) {}

function add(*user us) {};

function delete(*user us) {};

function adminLogin(*user us) {
}

function guestLogin(*user us) {
}
function customerLogin(*user us) {

}

// com O.O.
public void save(User us) {
	persister.save(us)
}

function login(username, password, type) {
		
    // Abstraction
    // Polymorphism
    // Encapsulation
    // Inheritance ... types
    
    Factory f = UserFactory.for(type);
    UserGuest us = f.login(username, password);
    
    User login(string username, string password);
    
    user.uploadXML() ts, net, java
    
    python, js e go. type duckying
    user.uploadXML()
    
    
    validUsers("jose")
    validUsers("jose", "joao", )
    
    long getId()
    string getUsername()
    
    if ("" != type) {
        // guest pointer
    }
    else if (typeAdmin == type) {
        // admin pointer
    }
    else if (typeCustomer == type) {
        // customer pointer
    }
    else if (typeGuest == type) {
        // guest pointer
    }


    // what if us.login()?
}

function login(request req) {
    *user us = userFrom(req)
    us.login()

    int type = getUserType(req)
    if (guest) {
        return guestLogin()
    }
    if (admin) {
        return adminLogin()
    }
    if (customer) {
        return customerLogin()
    }

    ..
    ..
    ..
}



==== paramos aqui

bases da orientação a objetos

=============================

dados + comportamento

// dados
user.c

const int typeAdmin = 0;
const int typeGuest = 1;
const int typeCustomer = 2;

struct user {
    int id;
    char[] name;
    int type;
    int role;
    int permission;
    *add;
}


//comportamento
user_management.c
function add(*user us) {};

function delete(*user us) {};

function adminLogin(*user us) {

}
function guestLogin(*user us) {

}
function customerLogin(*user us) {

}

function genericLogin(*user us) {
    if (typeAdmin) {
        // admin pointer
    }
    else if (typeCustomer) {
        // customer pointer
    }
    else if (typeGuest) {
        // guest pointer
    }

    // what if us.login()?
}

function login(request req) {
    *user us = userFrom(req)
    us.login()

    int type = getUserType(req)
    if (guest) {
        return guestLogin()
    }
    if (admin) {
        return adminLogin()
    }
    if (customer) {
        return customerLogin()
    }

    ..
    ..
    ..
}


function main(*args) {}

========================

//"comportamento + dados == O.O.P."

type admin {
    int id;
    string name;
    add();
    delete();
}

// Abstraction, Polymorphism, Encapsulation and Inheritance
// reuso, expressividade, manutenção, facil adicionar coisas

admin ~ guest ~ customer ~ batatinha ~ <user>
// erlang "se vc nao sabe o que chega pra vc, vc nao
// deveria interceptar"


// abstração pra reuso // type
user us = userFrom(req) //batatinha
delete(us)
create(us)

admin.login() ~ user.login() ~ guest.login() ~ customer.login()

user = admin
user = guest
user = customer
user.login() 

// herança
admin <-- user

// poli - morfismo

liskov => L (SOLID)

fundamentos que se reforçam em torno dos tipos: herança, polimorfismo, abstração e encapsulamento;

programaçao orientada a tipos!

para que tudo isso? reuso, facilidade de mudança, manutenção!

reuso,
facilidade de mudança,
isole o que varia


isole / esconde o que muda muito;
esconda tudo q nao precisa ser exposto;

// interface exposta
// interface, REST, exposed function
// contrato
interface UserService {
    Boolean login(Request req);
    void save(User user);
    void delete(User user);
}

// mudanças de contrato / assinatura propam
// software a fora
Boolean login(Request req, Context ctx) {
    XML body = extract(req)
    User loadUserFrom(body)
    return user.login()
        ? user
        : null;
}

nossas boas praticas de programação
===================================

reuso, facilitar manutenção, evitar erros ou propagação de bugs, etc

* DRY; Dont repeat yourself (reuso) <--- abstracao--->

loginAdmin
loginGuest
loginCustomer

login(user us)

---

* KISS (keep it simple) nao é fazer a primeira coisa que funciona;
por exemplo: tenho um usuario (no futuro eu POSSO ter, eu nao sei se terei outras implementações). Então porque preciso de uma interface;

* YAGNI - voce nao vai precisar disso mesmo!

* Isole / esconda o que varia;

* Codifique para contratos;
codifique pra interface ou classes abstratas;

// contrato / interface exposta
interface UserService {
    Boolean login(Request req);
    void save(User user);
    void delete(User user);
}

* Composition over inheritance

na herança voce herda tudo da classe mãe.

// herança nos proporciona
class MouseEventListener {

    protected _doClick()

    public onClick() {
        //..
        _doClick()
    }

    public mouseMove(event evt) {
        // ...
    }

}

class MouseListener extends MouseEventListener {

    protected _doClick()

    public onClick() {
        _doClick()
    }

    @override
    public mouseMove(event evt) {
        // do nothing
    }

}

// composicao nos proporciona

class click {
    void _doClick() {
        //
    }
}

class MouseListener implements EventListener {

    private click;

    public onClick() {
        this._doClick();
    }
}

class MouseEventListener implements EventListener {

    private click;

    public onClick() {
        this._doClick();
    }
}

* código com mesma granularidade;
  detalhes na historia ficam dentro dos capitulos;

por exemplo:

class OrderReport {

    // pdf com os pedidos do cliente
    PDF export(CustomerInfo info) {
        PDF pdf = new PDF();
        // cabecalho
        Header header = new Header();
        header.append(info.clientName());
        header.append(info.clientAddress());
        pdf.add(header);

        List<Orders> orders = dbInstance.listOrders(info.clientId);
        Content content = new Content();
        for(Order o: orders) {
            content.append(formatOrder(o));
        }
        pdf.add(content);

        // rodape
        Footer footer = new Footer();
        footer.append(new Date());
        pdf.add(footer);
        return pdf;
    }

}

class OrderReport {

    Header createHeaderFrom(CustomerInfo info) {
        Header header = new Header();
        header.append(info.clientName());
        header.append(info.clientAddress());
        return header;
    }

    Content createContentFrom(CustomerInfo info) {
        List<Orders> orders = dbInstance.listOrders(info.clientId);
        Content content = new Content();
        for(Order o: orders) {
            content.append(formatOrder(o));
        }
        return content;
    }

    Footer createFooterFrom(CustomerInfo info) {
        Footer footer = new Footer();
        footer.append(new Date());
        return footer;
    }

    // pdf com os pedidos do cliente
    public PDF export(CustomerInfo info) {
        Header header = createHeaderFrom(info);
        Footer footer = createFooterFrom(info);
        Content content = createContentFrom(info)
        
        PDF pdf = new PDF();
        pdf.add(header);
        pdf.add(content);
        pdf.add(footer);
        return pdf;
    }

}


class Factory {

    User from(String type) {
        if (userType.equals("admin")) {
            return new Admin(req.body);
        }
        if (userType.equals("guest")) {
            return new Guest(req.body);
        }
        if (userType.equals("customer")) {
            return new Customer(req.body);
        }
    }

}

class UserService {

    public User login(Request req) {
        String userType = req.body.userType;
        User loadedUser = new Factory().from(userType);
        return loadedUser.login();
    }

}

fazendo isso a nivel de pacotes e modulos gera a arquitetura de camadas. Onion model.




* SOLID

receitas / diretivas pra quem ta começando;

- S (SRP) - seu codigo faz uma cosia e so uma coisa

```python

class Pg:
    @static_method
    def newConnection() -> DbConnection:
        # new class pg
        # string connection host, password, user
        # return conn
        pass

class DB:
    @static_method
    def findUser(username: str, password: str):
        connection = Pg.newConnection()
        rs = Pg.query("select * from user where username = '{}'".format(self.username))
        return  rs.next()

class User:
    def login(self) -> bool:
        us = DB.findUser("user", self.username)
        return us and us.password == self.password
```

- O (open closed) aberto pra extensao e fechado pra mudanca

```python
class Admin(User):
    def login(self) -> bool:
        us = DB.findUser("user", self.username)
        return us and us.password == self.password and us.role == "admin
```

- L (Liskov) - classes / artefatos de mesmo tipo precisam ser compativeis. respeite o contrato.

```python
    # us.login()
    # admin -> us
    # guest -> us
    # admin.login()
    # guest.login()
    
    # heranca = tipagem + abstracao + reuso
class user:
    pass

class Admin(User):
    def login(self):
        pass

def login_():
    pass

us = User()
us.login()

adm = Admin()
adm.login()
```

- I - interface segregation

```java
interface MouseListener {

    public void mousePressed(MouseEvent e);

    public void mouseReleased(MouseEvent e);

    public void mouseEntered(MouseEvent e, boolean isDragAndDrop);

    public void mouseExited(MouseEvent e, boolean isDragAndDrop);

    public void mouseClicked(MouseEvent e);

}

public class MouseClickDemo implements MouseListener {

        public void mousePressed(MouseEvent e) {
       // DO NOTHING
    }

    public void mouseReleased(MouseEvent e) {
       // do nothing
    }

    public void mouseEntered(MouseEvent e, boolean isDragAndDrop) {
       // do nothing
    }

    public void mouseExited(MouseEvent e, boolean isDragAndDrop) {
       // do nothing
    }

    public void mouseClicked(MouseEvent e) {
       // codigo
    }

}

interface MouseClick {
    public void mousePressed(MouseEvent e);
    public void mouseReleased(MouseEvent e);
    public void mouseClicked(MouseEvent e);
}

interface MouseMove {
    public void mouseEntered(MouseEvent e, boolean isDragAndDrop);
    public void mouseExited(MouseEvent e, boolean isDragAndDrop);
}

interface MouseListener extends MouseClick, MouseMove {

}


public class MouseClick2 implements MouseClick {

    public void mousePressed(MouseEvent e) {
       // DO NOTHING
    }

    public void mouseReleased(MouseEvent e) {
       // do nothing
    }

    public void mouseClicked(MouseEvent e) {
       // codigo
    }

}
```

- D (dependency injection) springboot, .net core,  gerenciador de contexto

```python
    # pg = PostgresConnection() <-- nao queremos >
class DBConnection:
    pass

class Pg(DBConnection):
    @static_method
    def newConnection() -> DbConnection:
        # new class pg
        # string connection host, password, user
        # return conn
        pass

class DB:
    def findUser(username: str, password: str):
        connection = Pg.newConnection()
        rs = Pg.query("select * from user where username = '{}'".format(self.username))
        return  rs.next()

class User:
    def __init__(self, dbconnection: DbConnection):
        self.conn = dbConnection

    def login(self) -> bool:
        us = self.findUser("user", self.username)
        return us and us.password == self.password
```

```python
class User:
    def __init__(self, db_connection: DbConnection): # DI
        self.conn = db_connection

    def login(self) -> bool:
        us = self.conn.find_user("user", self.username)
        return us and us.password == self.password

class User:
    def __init__(self): # sem DI
        self.conn = Pg.new_connection()

    def login(self) -> bool:
        us = self.conn.find_user("user", self.username)
        return us and us.password == self.password

### usage

# codigo estatico
us = User()
us.login()

# so consegue biblioteca propria de mocks
assert(conexao_de_mentira().has.been.called())
assert(conexao_de_mentira().find_user().has.been.called())

# como testa?

# codigo com DI
us = User(Pg.new_connection()) # reuso pra aceitar outras conexoes e testes
us.login()

cn = conexao_de_mentira()
# teste
us1 = User(cn)
us.login()

us2 = User(cn)
us.login()

assert(conexao_de_mentira().has.been.called())
assert(conexao_de_mentira().find_user().has.been.called())
```

# codigo
```python
def connect(url, password, username):
    return Pg(url, password, username)

class UserControler:
    def __init__(self, db_connection DbConnection):
        self.conn = db_connection

# usage com codigo
api = UserController(connect(url, password, username))
```

# configuracao
```yaml
pg:
    url: ''
    password: ''
    username: ''

userControler:
    db_connection: pg

OrderControler:
    db_connection: pg
```

// projeto java com bancos em DB2, Oracle, Pg

+ pasta do projeto
--- executavel principal
--- biblioteca do banco de dados (db2 ou oracle ou pg)
--- config.yaml

# convencao
```yaml
userControler:
    db_connection: pg

OrderControler:
    db_connection: pg
```

+ ecommerce
-- controllers
    +--- user-controller.py
    +--- order-controller.py
-- repositories
    +--- user-repositories.py
    +--- order-repositories.py
-- tests

## Convencao > configuracao > codigo

# exemplo pratico do springboot como convencao
```java
package com.example.springboot;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

	@GetMapping("/")
	public String index() {
		return "Greetings from Spring Boot!";
	}

}


package com.example.springboot;

import java.util.Arrays;

import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.Bean;

@SpringBootApplication
public class Application {

	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}

}
```


Boas praticas de codigo:

- granularidade de funcoes, arquivo, modulo, diretorio, software


## Design Patterns


// esconder complexidade / SRP
### Factory - criacional

```python
class Formatter:
    def format(value: string) -> string:
        pass

class ANSIFormatter(Formatter):
    def format(value: string) -> string:
        return '1234' + value

class ZEBRAFormatter(Formatter):
    def format(value: string) -> string:
        return '^L\n^V1234\n^P' + value

class IntermecFormatter(Formatter):
    def format(value: string) -> string:
        return '^L\n^B1234\n^P' + value
    
def formatterFor(printer: string) -> Formatter:
    if (printer == 'Intermec'):
        return IntermecFormatter(1,0,1,1)
    
    if (printer == 'Zebra'):
        return ZEBRAFormatter()

    if (printer == 'ZBL'):
        return ZBLFormatter()

    return ANSIFormatter()

// usage
def print(value: string, printer: string) -> None:
    PrinterDevice device = PrinterDevice.instance(printer)
    Formatter fmt = formatterFor(printer)
    formattedValue = fmt.format(value)
    device.print(formattedValue)
    return None

    # if (printer == 'Intermec'):
    #     IntermecFormatter fmt = IntermecFormatter(1,0,1,1)
    #     device.print(fmt.format(value))
    #     return None
    
    # if (printer == 'Zebra'):
    #     ZEBRAFormatter fmt = ZEBRAFormatter()
    #     device.print(fmt.format(value))
    #     return None

    # if (printer == 'ZBL'):
    #     ZEBRAFormatter fmt = ZBLFormatter()
    #     device.print(fmt.format(value))
    #     return None

    # ANSIFormatter fmt = ANSIFormatter()
    # device.print(fmt.format(value))
    # return None


v// usage
print('banana', 'Intermec')
print('banana', 'Zebra')
print('banana', 'batatinha')
```

```python
class Factory: # SRP
    def configure(printer: string) -> Formatter:
        # <NomeImpressora>+Formatter() <=== convencao
        if (printer == 'Intermec'):
            return IntermecFormatter()
        
        if (printer == 'ZBL'):
            return ZBLFormatter()
        
        if (printer == 'Zebra'):
            return ZebraFormatter()

        if (printer == 'Epson'):
            return EpsonFormatter()
        
        if (printer == 'Kodak'):
            return KodakFormatter()

        return ANSIFormatter()

class LabelPrinter:
    // usage
    def print(value: string, printer: string) -> None:
        PrinterDevice device = PrinterDevice.instance(printer)
        Formatter fmt = Factory().configure(printer)
        formattedValue = fmt.format(value)
        device.print(formattedValue)
        return None

# KISS
class LabelPrinter:
    // usage
    def print(value: string, printer: string) -> None:
        PrinterDevice device = PrinterDevice.instance(printer)
        ZebraFormatter fmt = ZebraFormatter()
        formattedValue = fmt.format(value)
        device.print(formattedValue)
        return None
```

### Singleton - criacional

```java
//controller <-- rotas API
OrderController.class
//
Order o1 = req.getOrder()

OrderService.class
//service <-- regras de negocio (nao eh view e nao é banco)
// coordene sua execucao aqui
//repository [precisa de ORM] (Data Access Object) <--- dados >

OrderRepository.class
// repo
public interface OrderRepository extends JPARepository<Order> {
    public void save(Order o1);
}

Order o1 -> controller.save(o1) -> service.save(o1) -> ... -> repository.save(o1) -> db

public interface UserRepository extends JPARepository<User> {
    public List<User> findByUsername(String username);
}

public interface MessageRepository extends JPARepository<Message> {
    public List<Message> allMessages();
}

public interface FilterMessageRepository extends JPARepository<Message> {
    public default List<Message> allMessages( {
        UserRepository
        MessageRepository
    }
}
//query, projeta como resultado do tipo User
// `select * from User where username = :username`

DAO ----> repository
DAO <-//- repository

```


```java

public class PrinterConfiguration {

    private String defaultPrinterName;

    private Long printerResolution;

    //...

    private static PrinterConfiguration instancia = null;

    private PrinterConfiguration() {
        loadFromIniFile("~/print.ini")
    }

    // on demand
    // eager
    // thread safe
    // unsafe
    // economiza tempo de carga, ou economia espaco em memoria (economia de recursos)
    public static PrinterConfiguration getInstancia() {
        if (instancia == null) { // unsafe e on demand
            instancia = new PrinterConfiguration();
        }
        return instancia;
    }

    //eager e thread safe
    static {
        instancia = new PrinterConfiguration();
    }
    
    public static PrinterConfiguration getInstancia() {
        return instancia;
    }

    //thread safe e on demand
    public static synchonized PrinterConfiguration getInstancia() {
        if (instancia == null) { // unsafe e on demand
            instancia = new PrinterConfiguration();
        }
        return instancia;
    }

}

// usage
var config1 = PrinterConfiguration.getInstancia();
var config2 = PrinterConfiguration.getInstancia();

//true
(config1 == config2)

public class OrderService {

    private DBConnection connection = new Connection();

    public void save(Order o1) {
        connection = new Connection()
        // fazer qualquer coisa
        // connection.save() //final
        /// connection.save(o1);
    }

    public void validate(Order o1) {
        connection = new Connection()
        /// connection.save(o1);
    }
}

//spring (singleton)
public class OrderController {
    
    private OrderService service;

    public void save(Order o1) {
        //
        service.validate(o1)
        service.save(o1)
    }

}



```
// economiza de recursos
#### Singleton - Basico

#### Singleton - Thread Safe

#### Singleton - Lazy

#### Singleton - Eager

====

### Strategy - comportamental

### Template Method - comportamental

```java
//intermec, zebra, argox
class Printer {

    // v0
    public void print(String commands, String printerName) {
        // codigo
        String encoded = encode(commands)
        sendToPrinter()
        if (printerName.equals("intermec")) {
            // serial
            serial(encoded);
        }
        else if (printerName.equals("argox")) {
            // usb
            usb(encoded);
        }
        else if (printerName.equals("zebra")) {
            // network
            network(encoded);
        }
        else if (printerName.equals("CHINA")) {
            // BT
            bt(encoded);
        }

        // finalizacao (com popups)
        //tratamento de erros
    }

    // v1
    private int sendToPrinter(String encoded, String printerName) {
        int labels = 0
        if (printerName.equals("intermec")) {
            // serial
            labels = serial(encoded);
            // 
        }
        else if (printerName.equals("argox")) {
            // usb
            labels = usb(encoded);
        }
        else if (printerName.equals("zebra")) {
            // network
            labels = network(encoded);
        }
        else if (printerName.equals("CHINA")) {
            // BT
            labels = bt(encoded);
        }
        return labels;
    }

    public void print(String commands, String printerName) {
        // codigo
        String encoded = encode(commands)
        int count = sendToPrinter(encoded, printerName)
        //quantas etiquetas foram impressas
        // finalizacao (com popups)
        //tratamento de erros
    }

}

//v2
abstract class Printer {

    abstract int sendToPrinter(String encoded);

    public void print(String commands) {
        // codigo
        String encoded = encode(commands)
        int count = this.sendToPrinter(encoded)
        //quantas etiquetas foram impressas
        // finalizacao (com popups)
        outroMetodoAbstrato()
        //tratamento de erros
    }
}

class Intermec extends Printer {
    int sendToPrinter(String encoded) {
        // serial
        return serial(encoded);
    }
}

class Zebra extends Printer {
    int sendToPrinter(String encoded) {
        // network
        return network(encoded);
    }
}

class Argox extends Printer {
    int sendToPrinter(String encoded) {
        // usb
        return usb(encoded);
    }
}

class China extends Printer {
    int sendToPrinter(String encoded) {
        // BT
        return BT(encoded);
    }
}
// template method

// usage com 
interface i = new PrinterFactory.create(printerName);

new PrinterFactory.create(printerName).print(commands)

// reuso do BT
BT(arquivo) nao da pra fazer com template

//strategy

interface Sender {
    int send(String encoded);
} 

class Printer {

    private Sender sender;

    private void asciiToChar() {..do something};

    public void print(String commands) {
        // codigo
        String encoded = encode(commands)
        int count = this.sender.send(encoded)
        //quantas etiquetas foram impressas
        // finalizacao (com popups)
        outroMetodoAbstrato()
        //tratamento de erros
    }
}

class Intermec implements Sender {
    int send(String encoded) {
        // serial
        return serial(encoded);
    }
}

class Zebra implements Sender {
    int send(String encoded) {
        // network
        return network(encoded);
    }
}

class Argox implements Sender {
    int send(String encoded) {
        // usb
        return usb(encoded);
    }
}

class China implements Sender {
    int send(String encoded) {
        // BT
        return BT(encoded);
    }
}

// reuso BT
new Printer(new Zebra()).print(commands);
new China().send(banana)
```

### Strategy vs Template Method

template method se baseia na heranca, reusa funcoes da classe pai

strategy é baseado em composicao, tem melhor reuso, mas precisa que as implementacoes sejam bem separadas.

algoritmos com a seguinte estrutura
funcao () {
    //codigo q da pra reusar
    //codigo q da pra reusar

    //nao da pra reusar A
    //nao da pra reusar B
    //nao da pra reusar C

    //codigo q da pra reusar
    //codigo q da pra reusar
}

### padroes que delegam comportamento para uma dependencia interna:

// potencializar reuso

algoritmos com a seguinte estrutura
funcao () {
    //nao da pra reusar A
    //nao da pra reusar B
    //nao da pra reusar C

    //codigo q da pra reusar
    //codigo q da pra reusar
}

funcao () {
    //codigo q da pra reusar
    //codigo q da pra reusar

    //nao da pra reusar A
    //nao da pra reusar B
    //nao da pra reusar C
}

### Adapter (Wrapper) - estrutural

refactory / temporario

class PrinterV2 {
    int print(Page page);
}

class PrinterV1 {
    int print(String commands, String printerName);
}

class PrinterAdapterV2ParaV1 extends PrinterV1 {

    private PrinterV2 parent;

    @Override
    int print(String commands, String printerName) {
        page new Page(commands, printerName)
        return this.parent(page)
    }

}

v1 = new PrinterV1();
framework(v1);

// retrocompatibilidade

v1 = new PrinterAdapterV2ParaV1(new PrinterV2());
framework(v1);


// antecipar o uso antes de terminar o refactory
class PrinterAdapterV2ParaV1 extends PrinterV2 {

    private PrinterV1 parent;

    @Override
    int print(Page page) {
        return this.parent.print(page.commands, page.printerName);
    }

    @Override
    int print(String commands, String printerName) {
        page new Page(commands, printerName)
        return this.parent(page)
    }

}

v2 = new Printerv2();
webpagesV2(v2)

### Proxy - estrutural

// economia de recurso ---> deixar lazy, on demand

class DBConnection {
    public Statement createStatement();
}

class DBConnectionProxy extends DBConnection {

    private DBConnection parent = null;

    @Override
    public Statement createStatement() {
        if (parent == null) {
            parent = new DBConnection();
        }
        return this.parent.createStatement();
    };

}

### Decorator (for behavior) - estrutural

### Adapter vs Decorator vs Proxy



### Behavioral Patterns / Iterator | what about Generator?

### Creational Patterns / Builder

### Creational Patterns / Copy on constructor

### Creational Patterns / Prototype

### Prototype vs Builder

### Creational Patterns / Flyweight

### Creational Patterns / Object pool

### Prototype vs Object Pool vs Flyweight

### Behavioral Patterns / Command


### and more