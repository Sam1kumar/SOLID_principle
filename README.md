# SOLID principle

SOLID principle was developed by Rober C Martin (famous as Uncle bob).
SOLID stands for: -
1. S - Single Responsibility
2. O - Open for extension but closed for modification
3. L - Liskov Substitution Principle
4. I - Interface Segragation
5. D - Dependency Injection

These principle helps us establishing a practices for developing software that will be more managable and extensible. Adopting to these practices helps team to avoid code smells (any script or part of code that give sensation of blatant error), refactoring (modification in project without modifying the code), etc.

## Single Responsibility
This say that state or class should have only one responsibility.
### For Example, 

Let's say a program that is responsible for searching/filtering a data should be responsible for keeping or maintaining search/filter result. 
If you are making a search application, there are two ways to do that, 
1. First one is you will have a variable in the same class to store the result, where you have searched/filtered the data and, 
2. In second way, you will maintain two separate class for searching/filtering the data and storing it, this will avoid having a search/filter function where you need only to display the data and the best part is that you don't have to pass the result when you are switching page.

To understand it more, let's take another example of a class graph, a graph has a node and edge. One can easily implement graph, by either having list containing array of integer or two dimensional matrix but in either of those we can't modify the property of nodes, we are restricted to use number only.

    class node{
        ..//all the varible that a node stores + list of connected nodes.
        node(){} function to assign values to all the variable.
    }
  
    class graph{
        list<node> Nodes.
    
        .. // function to perform operation on graph like searching, counting connections, etc.
    }
    
 

## Open for extension but closed for modification
This says that a feature or functionality of class or state should be added without modifying the code.
### For Example,
In example of single responsibility, we have discussed about we should have seperate classes for graph and its node, in the implementation of graph. So, that we can extend any variable that we want to store in our node (because most of the operation of graph is done either using id or any unique variable in the node), without modifying the graph. In that example it's impossible to extend.

Now let's take an another example,
In an application there are more than 1-2 pages where we have to show loading animation where we load data, in most of pages loading animation are same. If we implement the loading animation where we have implemented the asynchrounous code, then it will create a havoc if we want to change the animation or there might be a situation loading animation plugin stops working in a new update, then we have to go to every page and then we have change every loading animation. On the other hand if we have used separate loading animation page then we have to change the code only at one place. Even if we want we can add more animation and use different animation where and however we like. 

            onPressed: () async{
                dynamic over = Overlay.of(context);
                OverlayEntry entry = OverlayEntry(

                  builder: (context) => Loading() //here we have used loading class here we also have a option to include the whole loading code that would violate open closed principle..
                );

                over.insert(entry);

                var client = http.Client();
                var url = Uri.parse('https://jsonplaceholder.typicode.com/users');
                var response = await client.get(url);

                dynamic users = await jsonDecode(response.body);

                entry.remove();
                Navigator.pushNamed(context, '/userList', arguments: users);
            },
              
              
            class Loading extends StatelessWidget {
            const Loading({Key? key}) : super(key: key);

            @override
            Widget build(BuildContext context) {
            return Container(
                    color: Colors.black45,
                    child: Center(
                      child: Container(
                        color: Colors.white,
                        width: 350.0,
                        height: 100.0,
                        child: Center(
                          child: SpinKitRipple(
                            color: Colors.black,
                            size: 100.0,
                          ),
                        ),
                      ),
                    ),
                  );
                }
            }

We can also think of theme colour of animation in one code theme is fixed while in other code we ask for color as parameter.
  

## Liskov Substitution Princple
This says that, a subclass or derived class should be able to substitute it's parent.

### For example
Let's take an example of vehicle interface/class that can be extended by different types of vehicle. (Here let's assume that every vehicle engine in the world starts in the same way)

    class Vehicle{
        int numberRiders;
        int numberPilot;
        
        move(){
            //code
        }
        
        startEngine(){
            //code
        }
    }
    
    class Car extends Vehicle{
        openDoor(){
            //
        }       
    }
    
In the above example if we want to implement cycle that don't have engine, then we have to throw an error, so, instead of having startEngine method in the vehicle class we should implement startEngine method in subclass of vehicle.

## Interface Segragation
One should program in such a way that, user should not be forced to implement a method of interface that he don't want to use.

### For example
Let's say there is a parent class computer now this class will be parent for desktop, laptop, server, micro-controller, etc. Now, some of them have peripherels like display, mouse, joysticks, sensor, etc. and common parts among them in cpu.
Now consider a interface computer.

    class Computer{
      //it will have virtual methods like
      cpuController();
      memoryManagement();
      display();//etc.. 
      readingSensor();
    }
    
Now if someone want to implement class called microcontroller that extends class computer, he has to unnecessarily implement methods display(). So, there sould be different interface for different types of computer not a interface for computer as follow or the we should not define virtual methods like display and readSensor, it should be implemented depending on the need.


## Dependency Injection or Dependency Inversion
This says that a class or state should depend only on it's parent class not on its subclass and abstaction should not depend on detail.

### For example
Now again take example Liskov substitution example, there I had assumed that startEngine method will be same for every vehicle, so implementing it in the vehicle itself is fine, but what if startEngine method is not same for all types of vehicle. Now in that code every vehicle have to depend on the startEngine method of vehicle class will throw an error and violate **D** principle. So, to avoid any error we should only declare startEngine method as follow, in that way every vehicle don't have to depend on class vehicle.

    class Vehicle{
        int numberRiders;
        int numberPilot;
        
        move(){
            //code
        }
        
        startEngine();
    }
    
    class Car extends Vehicle{
        openDoor(){
            //
        }
        
        startEngine(){
            //
        }
    }
    

    
    
    
    
    
    
    
    
    
    
    
    
    
