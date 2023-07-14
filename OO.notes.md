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

// proxy como cache com classes

```java
class Config {
    public boolean isDebugEnabled() {
        readFromFile('[debug]'); // simulando operacao de IO custosa
    }
}

class CacheableConfig extends Config {

    private Config parent;

    private Map<String, boolean> cache = new WeakHashMap<>();

    @Override
    public boolean isDebugEnabled() {
        if (!cache.has("debug")) {
            boolean result = parent.isDebugEnabled(); // simulando operacao de IO
            cache.put("debug", result);
            setTimeout(300* 1000, () -> {
                cache.remove("debug");
            })
        }
        return cache.get("debug");
    }

    public void purge() {
        cache.clear();
    }

}


//usage

Config cfg = new CacheableConfig(new Config());
cfg.isDebugEnabled() // le o disco e salva no cache
cfg.isDebugEnabled() // le o cache
cfg.isDebugEnabled() // le o cache
cfg.isDebugEnabled() // le o cache
cfg.isDebugEnabled() // le o cache
cfg.isDebugEnabled() // le o cache

//purge
LRU // mais recentes utilizados
LCU // mais comumentes utilizados

java // LinkedHashMap()
//removeEldestEntry(Map.Entry<K,V> eldest)
//Returns true if this map should remove its eldest entry.

Map<string, string>, Dictionary<string, string> ...
WeakMap // linguagens que possuem garbage collector
// gc pode recolher o que esta aqui dentro se precisar


Supplier<T> // T é o tipo do seu cache

T Cacheable<T>(Supplier<T> sup, String key) {
    if (!cache.has(key)) {
            boolean result = sup.get()
            cache.put(key, result);
            setTimeout(300* 1000, () -> {
                cache.remove(key);
            })
        }
        return cache.get(key);
    return 
}


delegate Supplier T ();

T Cacheable<T>(Supplier<T> sup, String key) {
    if (!cache.has(key)) {
            boolean result = sup.get()
            cache.put(key, result);
            setTimeout(300* 1000, () -> {
                cache.remove(key);
            })
        }
        return cache.get(key);
    return 
}

//usage
public boolean isDebugEnabled() {
    return Cacheable(
        () -> new Config().isDebugEnabled(),
        '[debug]'
    )
}
return 

```
// cache como proxy no python
```python
import functools
def lru_cache(fn): // curried function
    def wrapped(**args, **kargs):
        if to_string(args, kargs) not in cache:
            cache[to_string(args, kargs)] = fn(args, kargs)

        return cache[to_string(args, kargs)]

@lru_cache
def is_debug():
    return readFile('[debug]')

```

### Decorator (for behavior) - estrutural

```html
<b><s><p>banana</p></s></b>
```

Tag t = new B(new S(new P("banana")))
t.print() // => '<b><s><p>banana</p></s></b>'

```java
interface Tag {
    public String print();
}

// terminador
class P implements Tag {
    private String content;

    public String print() {
        return "<p>" + content + "</p>";
    }
}

class B implements Tag {
    private Tag next;

    public String print() {
        return "<b>" + next.print() + "</b>";
    }
}

class I implements Tag {
    private Tag next;

    public String print() {
        return "<i>" + next.print() + "</i>";
    }
}
```


```html
<b><p>banana</p></b>
```

```html
<i><p>banana</p></i>
```

```html
<em><p>banana</p></em>
```

```java
class Em implements Tag {
    private Tag next;

    public String print() {
        return "<em>" + next.print() + "</em>";
    }
}
```

```java
class XMLExporter implements Exporter {

    public String export(Report repo) {
        return ..."";
    }
}

class PDFExporter implements Exporter {

    private Exporter next;

    public String export(Report repo) {
        return new ToPDF(next.export(repo));
    }
}

class Em implements Tag {
    private Tag next;

    public String print() {
        return "<em>" + next.print() + "</em>";
    }
}
```

```python

class P:
    def render():
        if temI
            //
            if temB
                //
            
            else

        if temB
            if temI

            else

        if temS
            if temB
                if temI

                else
            else

```

<!-- /calculando preco com varias variaveis -->
```java
class Calculator implements  {
    public float calculaValorACobrar(Cliente cliente, Pedido pedido) {
        float total = pedido.getTotal();
        if (temFrete(cliente)) {
            total += calculaFrete(pedido, cliente)
        }
        if (temCupom(cliente)) {
            total += calculaCupom(pedido, cliente)
        }
        if (temImposto(cliente)) {
            total += calculaImposto(pedido, cliente)
        }
        return total;
    }
}
```

// reusando blocos com precos
```
public interface Calc {
    public float calculaValorACobrar(Cliente cliente, Pedido pedido);    
}

class Calculator implements Calc {
    public float calculaValorACobrar(Cliente cliente, Pedido pedido) {
        return pedido.getTotal();
    }
}

class ComFrete implements Calc  {
    private Calc next;

    public float calculaValorACobrar(Cliente cliente, Pedido pedido) {
        if (temFrete(cliente)) {
            return next.calculaValorACobrar(Cliente cliente, Pedido pedido) - calculaFrete(pedido, cliente);
        }
        return return next.calculaValorACobrar(Cliente cliente, Pedido pedido);
    }
}

// usage sempre posso criar com todos

new ComImposto(new ComFrete(new Calculator()));

// sem os condicionais
class ComFrete implements Calc  {
    private Calc next;

    public float calculaValorACobrar(Cliente cliente, Pedido pedido) {
        return next.calculaValorACobrar(Cliente cliente, Pedido pedido) - calculaFrete(pedido, cliente);
    }
}

// factory pra decidir o que criar
Calc c = factory.create(cliente)


```
// agora eu quero fidelidade na cobranca tb

// decorator

quadros (tela - desenho, moldura, vidro, ganchos q seguram na parede)
minimo necessario - tela

tela + moldura = quadro
tela + moldura + vidro = quadro

if (vidro)
if (moldura)
if (moldura && vidro)


moldura + vidro + ganchos

<i><b><p>banana</p></b></i>



#### exemplo melhor de decorator

- seu software pode receber um json

```json
{
    "pedido": 123456789,
    "nome": "jteodoro",
    "endereco-entrega": "av. batatinha, 234",
    "cep": "02304-000"
}
```

```separado por linhas
123456789
jteodoro
av. batatinha, 234
02304-000
```

```base64
eyJwZWRpZG8iOiAxMjM0NTY3ODksIm5vbWUiOiAianRlb2Rvcm8iLCJlbmRlcmVjby1lbnRyZWdh
IjogImF2LiBiYXRhdGluaGEsIDIzNCIsImNlcCI6IjAyMzA0LTAwMCJ9Cg==
```

```zip
��Z����`��� �UA}f�j{ƞ�瘚ϓ��1s�"�ާ� �i�79�ӆ�Ote:##Ú�8�Ah�dD
```

zip + base64 = '77+977+9Wu+/ve+/ve+/ve+/vWDvv73vv73vv70g77+9VUF9Zu+/vWp7xp7vv73nmJrP++/ve+/vTFz77+9Iu+/vd6n77+9IO+/vWnvv703Oe+/vdOG77+9T3RlOiMjw5rvv70477+9QWjvv71kRAo='


input pode ser qqer desses:

json + base64
lines + base64
json + zip + base64
lines + zip + base64
xml + base64


output: zpl

mas eu imprimo uma etiqueta a partir do JSON. entao preciso transformar qualquer dessas cosias em json.

```typescript

interface Order {
    "pedido": number;
    "nome": string;
    "endereco-entrega": string;
    "cep": string;
}

const invokeMyThermalPrinter = (commands: ZPL) : void {
    // envia ZPL para impressora
}

const format = (content: string) : ZPL {
    // linguagem de comandos que a impressora entende
    return `
^XA
^FO40,25^FS
^LH200,100
^CF0,30
^FO35,13^FD{${content.nome}}^FS
^FO25,13^FD{${content.endereco}}^FS
^PQ1
^XZ
`
}

const stringToOrder = (content: string): Order {
    return JSON.parse(content)
}

// recursao ao infinito e alem

// content zipado print(content_zipado) => print(content_unziped) => print(content_lines_to_json)
// loop infinito => stack overflow
const print = (content: string) : void {
    if (isZip(content)) {
        // unzip
        return print(unzip(content));
    }
    if (isBase64(content)) {
        // decode
        return print(decode(content));
    }
    if (IsLineBasedString(content)) {
        // decode
        return print(createJSON(content));
    }
    if (IsXML(content)) {
        // decode
        return print(unmarshal(content));
    }

    Order order = stringToOrder(content)
    return invokeMyThermalPrinter(format(order))
}
```

```typescript

const terminator = function (content: string) : void;

// sempre recebo um json na string
// print é um terminator
const print = (content: string) : void {
    Order order = stringToOrder(content)
    return invokeMyThermalPrinter(format(order))
}

//decorator
// terminator(terminator)
const printZipped = (next: terminator) : any {
    // return new funtion
    // terminator
    return (content: string) : void {
        const unzipedContent = unzip(content)
        return next(unzipedContent)
    }
}

const printBase64 = (next: terminator) : any {
    // return new funtion
    // terminator
    return (content: string) : void {
        const decodedContent = decode(content)
        return next(decodedContent)
    }
}

const printLines = (next: terminator) : any {
    // return new funtion
    // terminator
    return (content: string) : void {
        const jsonContent = linesToJsonLike(content)
        return next(jsonContent)
    }
}

const printXML = (next: terminator) : any {
    // return new funtion
    // terminator
    return (content: string) : void {
        const unmarshledContent = xmlToJsonLike(content)
        return next(unmarshledContent)
    }
}

// (content: string) : void
print(meuConteudo)

// curry
// (content: string) : void
const fn1 = printZipped(print)
fn1(meuConteudo) --- json + zip

const fn2 = printBase64(print)
fn2(meuConteudo) -- json + base64

const fn3 = printBase64(printZipped(print))
fn3(meuConteudo) -- json + zip + base64

const fn4 = printBase64(printZipped(print))
fn4(meuConteudo) -- json + base64 + zip

printLine(print)

const fn5 = printBase64(printZipped(printLine(print)))
fn5(meuConteudo)

// return (content: string) : void
const factory = (content: string): terminator {
    let fn = print;
    if (isZip(content)) {
        fn = printZipped(fn)
    }
    if (isBase64(content)) {
        fn = printBase64(fn)
    }
    if (IsLineBasedString(content)) {
        // decode
    }
    return fn
}

const imprimir = factory(meuConteudo)
imprimir(meuConteudo)

```

### Adapter vs Decorator vs Proxy

// pedaco de algoritmo que eu delego pra alguem
// os objetos sao do mesmo tipo

// adapter -- retrocompatibilidade (refactory, evolucao de versoes)

//proxy -- economia de recursos

// decorator -- quando temos muitos IFs aninhados e compostos

### Behavioral Patterns / Iterator | what about Generator?

// sequence bancos de dados?
// cada vez q chama ela te da outro valor
// pk: 1, pk: 2, pk: 3 ....
// um conjunto de valores que precisa ser processado / encaminhado pra frente

sequence / generator
// back pressure ()
// seguro pra concorrencia (acessando um recurso que nao é segura pra concorrencia)

```javascript
const arrayNameFiles = ["f1.txt", "f12.txt","f11.txt", "f51.txt"]
// iterator
arrayNameFiles.forEach(f => {
    fs.readFileSync(f)
    // faco mais algo
})
// iterators
// for Each, for in, stream, select / where

const ids = []
// thread diferente
ids.push(idJteodoro)
// thread diferente
ids.push(idFabricio)
// thread diferente
ids.push(idPietra)

// !!race condition

// removendo race conditions com generators
gen = generator(ids)
// thread diferente
gen(idJteodoro)
// thread diferente
gen(idFabricio)
// thread diferente
gen(idPietra)

// semaforo, controle de concorrencia + backpressure
// .net, js, stream (criar a partir daqui), python

```

```c#
Factory.CreateBy(type) // factory esconde complexidade
// if Base64
// if PlainText
// if zip
// tudo fica escondido
```

```
objectExistente.Build()
objectExistente.Clone()
// construo um objeto a partir de uma configuracao ja definida

Builder, Prototype, CoC

// tem uma funcao que a partir de uma configuracao (dados de um objeto) conseguem criar um
objeto novo
```

// ideia central: ter uma configuração defina pra criacao de um objeto

### Creational Patterns / Prototype

// pra que serve: economizar recurso custoso de se carregar
//                  pra gerar concorrencia segura
//                  potencializa abstracao

```java
public class User {
    
    private DBAccess db;
    private Image photo; // custoso de carregar do disco, ou precisa pegar via internet
    private List<Address> addresses;

    // copia rasa
    public User shallowClone() {
        User us = new User();
        us.db = new DBAccess()
        us.photo = this.photo;
        us.addresses = this.addresses;
        return us;
    }

    // copia profunda
    // so mantem tipos primitivos
    public User deepClone() {
        User us = new User();
        us.db = new DBAccess()
        us.photo = new Image(this.photo);
        us.addresses = new List<>(this.addresses);
        return us;
    }
}

public class Admin extends User {
    @Overrride
    public Admin deepClone() {} // faz outra coisa

};
public class Guest extends User {};
public class Customer extends User {};
public class Employee extends User {};

// shallow copy (copia rasa)
// usage
User copy = userJose.clone()
copy.getImage().clear() // area compartilhada de escrita
copy.getAddresses().clear() // area compartilhada de escrita

// reuso de recurso

// deep copy (copia profunda)
// usage
User copy = userJose.clone()
copy.getImage().clear() // area isolada
copy.getAddresses().clear() // area isolada


// suponha que user tem metodos nao sao threadsafe (seguros pra rodar de modo concorrente)
List<String> addresses = user.addresses;
addresses.sort() // ordenacao in-place
addresses.find()

FindFirstAlpha(u => {
    u.addresses.sort();
    return u.addresses.first();
})

users.stream().map(FindFirstAlpha) // problema de concorrencia
users.stream().map(u => u.deepClone()).map(FindFirstAlpha) // nao tem problema de concorrencia

new Guest().deepClone() ==> <Guest>
new Admin().deepClone() ==> <Admin>
new User().deepClone() ==>  <User>
// oq ue eu quer é: obj.deepClone() e me retornar alguem

// nao precisamos fazer o seguinte:
    if admin
    new Admin(u)
    if user
    new User(u)
    if guest
    new Guest(u)
```

### Creational Patterns / Copy on constructor

```java
public class User {
    private DBAccess db;
    private Image photo; // custoso de carregar do disco, ou precisa pegar via internet
    private List<Address> addresses;

    public User() {}
}

public class User {
    private DBAccess db;
    private Image photo; // custoso de carregar do disco, ou precisa pegar via internet
    private List<Address> addresses;

    public User() {}
}

public class SU extends User {

    public SU() {}

    public SU(User existent) {
        this.setPhoto(new Image(existent.getPhoto()));
        this.setAddresses(new List<>(existent.getAddresses()));
    }
}

public class Guest extends User {};
public class Customer extends User {};
public class Employee extends User {};

//usage
users.stream().map(u => new SU(u))....
```

### Creational Patterns / Builder
// classe tem muitos campos, consigo criar valores default para classes com muitos campos
// simplificar chamada
//  chamada fluente

```java
public class UserBuilder {
    private DBAccess db = CentralConfig.getInstance().readOnlyAccess(); // db somente leitura por default
    private Image photo = GenericImage.getInstance(); // imagem default com a silhueta de um usuario
    private List<Address> addresses = new List<>();

    // demais withs

    public UserBuilder withAddresses(Address ... args) {
        this.addresses = new LinkedList<>(args);
        return this;
    }

    public User build() {
        // crio o objeto que me interessa
        return new User(db, photo, addresses);
    };
}

// usage
User us = new UserBuilder()
            .withDB(algumDB)
            .withImage(batatinha)
            .withAddresses(homeAddress, workAdress)
            .build();

User us = new UserBuilder().build();

// Lib lombok
// gera codigo do builder pra vc

//usando lombok

@Builder
public class Guest extends User {

};

// ultimo caso
// seu codigo define o builder
// mas nao é seu codigo que cria o objeto
// builder mais com cara de DTO (so os dados pra criar o objeto de verdade)

// caller 
UserBuilder builder = new UserBuilder()
            .withDB(algumDB)
            .withImage(batatinha)
            .withAddresses(homeAddress, workAdress);

// faria suas chamadas internas
invokeSeuCodigo(builder)

// da pra criar varias copias
builder.build()
builder.build()
builder.build()
builder.build()
```

### Prototype vs Builder vs Copy on constructor

// prototype (sempre trabalha dentro da mesma classe)
- economizar recurso
- garantir seguranca pra concorrencia
- esconder o tipo atras uma assinatura

// copy on constructor (trabalha com classes diferentes)
- criar um objeto em outra classe completamente diferente
- ajuda o SRP por nao dispersar codigo de construcao pelo software

// builder
- facilitar e simplificar a chamada (valores default, codigo fluente)
- quem cria a configuracao (dados do objeto) nao é quem dá o new no objeto

### Creational Patterns / Flyweight

- economizar recurso (seja tempo de carga, seja de memoria)
- Muito parecido com prototype

```java
public class User {
    private DBAccess db;
    private Proxy<Image> CompanyProfilephoto; // custoso de carregar do disco, ou precisa pegar via internet
}

public class OrderReport {
    private Proxy<Image> CompanyProfilephoto; // custoso de carregar do disco, ou precisa pegar via internet
}

public class ResourceRegister {
    private Map<String, Proxy<Image>> proxies; // proxy como cache

    public ResourceRegister getInstance() {} // singleton

    public get(String companyName) {
        if (!proxies.has(companyName)) {
            proxies.put(companyName, new Proxy<Image>(File.load(companyname+".png")))
        }
        return proxies.get(companyName);
    }
}

// User user = new user(); // image1
// OrderReport orderReport = new OrderReport(); //image1
orderReport.CompanyProfilephoto = ResourceRegister.getIntance().get(company) // somente leitura
user.CompanyProfilephoto = ResourceRegister.getIntance().get(company) // somente leitura
```

- flyweight trabalha com tipos de diferentes, classes diferentes e compartilha recursos entre elas.
- diferenca: forca para que todos os objetos compartilhados sejam somente leitura;

### Creational Patterns / Object pool

- reutilizar recursos escassos (numero fixo)
- evita conflito de concorrencia
- garantir que todo mundo tenha o seu de executar
- controla a quantidade e inicializacao desses objetos

// pool de celulares numa geladeira para realizacao de testes
```
[jose,                               Bruno]
[teodoro,  Elinaldo, ]
[iphone15, iphoneSE, O, O, O, O,   Android12]
```

// pool conexoes de bancos dados (limitadas!)
- conexao de bancos de dados sempre prontas;
- controlamos o numero maximo de conexoes abertas;
- economizar recurso pra nao deixar sempre o maximo de conexoes abertas;

```
{
    minConnections: 2,
    maxConnections: 10,
    maxTimeIdle: "60 seconds"
}
```

pool = [pg1, pg2(elinaldo), p3, ... p10];

// pool de impressoras (spool.exe)
- cria uma fila pra imprimir uma pessoa de cada vez

### Prototype vs Object Pool vs Flyweight

Prototype:

- economiza recurso custoso de se instanciar ou que consome muita memoria;
- smpre clona o mesmo tipo de objeto
- RW, R (de preferencia, somente leitura)

Flyweigth:

- economiza recurso custoso de se instanciar ou que consome muita memoria;
- compartilha o recurso em classes diferentes;
- somente leitura (muitas classes podem mexer na mesma variavel compartilhada, por isso é mais saudavel manter somente leitura)
- register de cache / proxy

Object Pool:

- economiza recurso custoso;
- recurso que é escasso;
- controla a concorrencia, mas tambem garante tempo de execucao pra todo mundo;

## Behavioral Patterns / Command

// muito usado pra enviar comandos pra devices antigos;

```js
user us = new User({name: 'jteodoro'});
us.create();

const command = {
    'action': 'user-created',
    'params': {
        'name': 'jteodoro'
    }
}
```

REST:
    POST, PUT
    GET,
    DELETE

## Behavioral Patterns / Observer

## Distributed Systems / Messaging and event source

## Distributed Systems / Pub & Sub

## Distributed Systems / Saga


## Structural Patterns / Bridge

## Structural Patterns / Facade

## Behavioral Patterns / Chain of Responsibility (CoR)

## Behavioral Patterns / Visitor

### and more