# Acces Modifiers

An acces modifier in java *specifies the accesibility of a class, package, method, field, scope, constructor or variable.*

**There are 4 types of modifiers: Public, Private, Protected and null**

## Public
    > A public modifier is accesible for every class, subclass, method, etc *since its on the same package*. 
    > In java, packages are all private by default, so if you need to use a public class in another package,
     you need to import that, using something like this:
     
.
     
    package bruh;
    
    public class Bruh{
     public String example;
     public int number;
     public double numberButDouble;
    
    }

꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱

     package bruh2;
     
     import java.com.bruh.Class

     public class Bruh2{
        public static void main(String[] args){
          Class.example = "yo angelo yo angelo yo angelo is this a motherfucking jojo reference";
          Class.number = 3141;
          Class.numberButDouble = 3.14159;
          
          String s = class.example;

          System.out.println(s);
        } 
      
      
     }

꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱
       
       In another words, you need to import the class and use the "nameOfTheClass.nameOfTheField".
      
## Private
    > A private modifier is accesible only for his own class. In another words, you cannot acces it from other files, but you can use the ENCAPSULTAION pattern.
    > Using encapsulation, you create public get and set methods that return or change the value of the private field, like this:

.

       pakcage iDontHaveIdeasForNames;
       
       public class Encapsulation{
          private String privateS;
          private int privateNumber;
          private double privateDouble;
          
          public Encapsulation(){
          
          }
          
          public getPrivateS(){
            return this.privateS;
          }
          
          public setPrivateS(String string){
            this.privateS = string;
          }
          
          public getPrivateNumber(){
            return this.privateNumber;
          }
          
          public setPrivateNumber(int number){
            this.privateNumber = number;
          }
          
          public getPrivateDouble(){
            return this.privateDouble;
          }
          
          public setPrivateDouble(double dbl){
            this.privateDouble = dbl;
          }
      }
      
    > In another words, you need to create public methods receiving an variable and setting the field with the variable (or, in a get method, just returning the field)

# Protected
    > A protected modifier is accesible only by subclasses and files on the same package, if you need to acces it from another class, you need to use inheritance, like this:
   
   .
   
        package inheritance;
        
        public class Entites{
          protected String protectedS;
          protected int protectedNumber;
          protected double protectedDouble;
          
          Entities(String s, int nmb, double dbl){
            this.protectedS = s;
            this.protectedNumber = nmb;
            this.protectedDouble = dbl;
          }
          
        }
        
꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱꠵꠱
        
        package idk;
        
        import inheritance.Inheritance;
        
        public class Son extends Inheritance{
          public String s = "a";
          public int i;
          public double d;
          
          public void Result(String s, int i, double d){
            super(s, i , d); //this line calls the super() method from Inheritance file. Since this one doesnt have an superclass, it uses the superclass from the extended file.
          }
          
          
          public void Show(){
            System.out.println(protectedS);
            System.out.println(protectedNumber);
            System.out.println(protectedDouble);
          
          }

        }
      

# No modifier
    > WHen there is no modifier, it is accesible by the class, package and subclass at the same package.


