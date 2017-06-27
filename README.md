import java.util.*;
class solution4
{
    public static void main(String[] args)
    {
        Reservation reserve = new Reservation(); 
        Person thread1 = new Person(reserve, 1); 
        thread1.start();
        Person thread2 = new Person(reserve, 2);
        thread2.start();
        Person thread3 = new Person(reserve, 3);
        thread3.start();
    }
}

class Reservation
{

    static int availableSeats = 10;

    synchronized void reserveSeat(int requestedSeats) 
    {
        System.out.println(Thread.currentThread().getName() + " entered.");
        System.out.println("Availableseats : " + availableSeats + " Requestedsetas : " + requestedSeats);
        if (availableSeats >= requestedSeats)
        {
            System.out.println("Seat Available. Reserve now :-)");
            try
            {
                Thread.sleep(100);  
            }
            catch (InterruptedException e)
            {
                System.out.println("Thread interrupted");
            }
            System.out.println(requestedSeats + "names" );
            Scanner obj=new Scanner(System.in);
		String arrayOfNames[] = new String[requestedSeats];
		for (int i = 0; i < arrayOfNames.length; i++) {
			System.out.print("Enter the name of passengers " + (i+1) + " : ");
		        arrayOfNames[i] = obj.nextLine();
		}
            availableSeats = availableSeats - requestedSeats;
           System.out.println("Number of seats booked are "+ requestedSeats);
          
        }
        else
        {
            System.out.println("Requested seats not available :-(");
        }
        System.out.println(Thread.currentThread().getName() + " leaving.");
        System.out.println("----------------------------------------------");
    }
}

class Person extends Thread
{

    Reservation reserve;
    int requestedSeats;

    public Person(Reservation reserve, int requestedSeats)
    {
        this.reserve = reserve;
        this.requestedSeats = requestedSeats;
    }
    public void run() 
    {
        reserve.reserveSeat(requestedSeats);
    }
}
