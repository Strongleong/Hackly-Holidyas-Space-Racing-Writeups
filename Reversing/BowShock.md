# BowShock

## Challenge Information
Bow shock is an amazing phenomenon, but you better not get too close…

### Flag 1 [50 points]:
#### BowShock

#### Description:
Can you find out how to minimize bow shock and prevent everything from turning into dust?

#### Solution:
Since there is a jar file, I go to an online decompiler, and I get a java file. The java file gives me what I need:

```
  
  public static int getInput() {
    int i;
    System.out.println("Set the amount of plasma to the correct amount to minimize bow shock: ");
    Scanner scanner = new Scanner(System.in);
    while (true) {
      try {
        i = scanner.nextInt();
        break;
      } catch (InputMismatchException inputMismatchException) {
        System.out.print("Invalid input. Please reenter: ");
        scanner.nextLine();
      } 
    } 
    totalInput += i;
    return i;
  }
  
  public static void bowShock() {
    System.out.println("And all was dust in the wind.");
    System.exit(-99);
  }
  
  public static void main(String[] paramArrayOfString) {
    System.out.println("Oh damn, so much magnetosphere around here!");
    if (getInput() != 333)
      bowShock(); 
    System.out.println("We survive another day!");
    if (getInput() != 942)
      bowShock(); 
    if (getInput() != 142)
      bowShock(); 
    System.out.println("Victory!");
    System.out.println("CTF{bowsh0ckd_" + totalInput + "}");
  }
}

```

Since 333+942+142 = So we simply get our solution as "CTF{bowsh0ckd_1417}"

**FLAG**: CTF{bowsh0ckd_1417}
