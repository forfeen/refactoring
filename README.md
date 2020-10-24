# Refactoring

## CoinPurse
From Chananya's CoinPurse code : https://github.com/OOP2020/coinpurse-forfeen

**main() Method**

in the `coinpurse/Main.java` class

https://github.com/OOP2020/coinpurse-forfeen/blob/master/coinpurse/Main.java

consider this code: 
```
public static void main( String[] args ) {

        *Initialize a variable*

        if (capacity < 0){
            error("It must be a non-negative integer.");
        }
        if (strategy.equals("recursive") ) {
            Purse purse = new Purse(capacity);
            ConsoleDialog ui = new ConsoleDialog(purse);
            purse.setWithdrawStrategy(new RecursiveWithdraw());
            System.out.printf("creates a Purse with capacity %d that uses RecursiveWithdraw.\n",capacity);
            ui.run();
        } else if (strategy.equals("greedy")) {
            Purse purse = new Purse(capacity);
            ConsoleDialog ui = new ConsoleDialog(purse);
            purse.setWithdrawStrategy(new GreedyWithdraw());
            System.out.printf("creates a Purse with capacity %d that uses GreedyWithdraw.\n",capacity);
            ui.run();
        } else {
            error("Error: invalid value for strategy");
        }
    }
```

- Refactoring Signs:
    - the "if" expression is long and complex.
    - many calls to `Purse class`, `ConsoleDialog class` and `ui.run()`.

- Refactoring: replace type code or “switch” with strategy

```
public static void main( String[] args ) {

        *Initialize a variable*

        if (capacity < 0){
            error("It must be a non-negative integer.");
        }
        Purse purse = new Purse(capacity);
        ConsoleDialog ui = new ConsoleDialog(purse);
        switch (strategy) {
            case "recursive" :
                purse.setWithdrawStrategy(new RecursiveWithdraw());
                System.out.printf("creates a Purse with capacity %d that uses RecursiveWithdraw.\n",capacity);
            case "greedy" :
                purse.setWithdrawStrategy(new GreedyWithdraw());
                System.out.printf("creates a Purse with capacity %d that uses GreedyWithdraw.\n",capacity);
        }
        ui.run();
    }
```