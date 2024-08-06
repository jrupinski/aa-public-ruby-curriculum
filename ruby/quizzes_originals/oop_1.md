# OOP Quiz 1

```ruby
  class Dance
    attr_reader :style

    def initialize(style = "Tap")
      @style = style
    end
  end

  class Ballet < Dance
    def initialize(technique)
      @technique = technique
      super("Ballet")
    end
  end

  class Swing < Dance
    def initialize(form)
      @form = form
      super
    end
  end

  bolshoi = Ballet.new("Vaganova")
  west_coast_swing = Swing.new("West Coast")
```

<quiz>
  <question>
    <p>Consider the above code. What are the respective return values from calling `bolshoi.style` and `west_coast_swing.style`?</p>
    <answer>`"Tap"`, `"Tap"`</answer>
    <answer>`"Ballet"`, `"Tap"`</answer>
    <answer correct>`"Ballet"`, `"West Coast"`</answer>
    <answer>`"Vaganova"`, `"Ballet"`</answer>
    <answer>`"Vaganova"`, `"West Coast"`</answer>
    <explanation>When called without any arguments (as in `Swing#initialize`), the `super` keyword will take all the arguments passed in to the current method and pass them as arguments to the parent class's version of the method. So `west_coast_swing` will have its `@style` set to "West Coast", i.e., the argument originally passed in to `Swing#initialize`. The `Ballet` class, however, does specify an argument for `super` to pass to its parent `Dance` class: "Ballet". `bolshoi`'s `@style` will accordingly be set to "Ballet". </explanation>
  </question>
</quiz>



```ruby
  class EngineStalledError < StandardError
  end

  class CollisionOccurredError < StandardError
  end

  def drive_car
    # engine may stall, collision may occur
  end

  begin
    drive_car
  rescue EngineStalledError => e
    puts "Rescued from engine stalled!"
    retry
  rescue CollisionOccurredError => e
    puts "Rescued from collision!"
  ensure
    puts "Car stopped."
  end
```

<quiz>
  <question>
    <p>Consider the above example. The first time `drive_car` is called, an EngineStalledError is raised! What happens next?</p>
    <answer>The program outputs `"Rescued from engine stalled!"` then `"Car stopped."`</answer>
    <answer>An uncaught error is thrown</answer>
    <answer correct>The program outputs `"Rescued from engine stalled!"` then retries running the code block </answer>
    <answer>The program outputs `"Car stopped."`</answer>
    <explanation>After rescuing the `EngineStalledError` this code block will hit the `retry` keyword.</explanation>
  </question>
</quiz>



```ruby
  class BoxOffice
    def initialize(num_seats, show_title)
      @num_seats = num_seats
      @show_title = show_title
      @tickets_sold = 0
    end

    def sell_ticket
      # logic for the ticket selling process goes here

      update_tickets_sold
    end

    private

    def update_tickets_sold
      @tickets_sold += 1
    end
  end

  tkts = BoxOffice.new(2000, "Rent")
```

<quiz>
  <question>
    <p>Consider the above code. Which of the following is a valid way to increase the number of `tkts` tickets sold by 1?</p>
    <answer>`tkts.update_tickets_sold`</answer>
    <answer>`BoxOffice.update_tickets_sold`</answer>
    <answer correct>`tkts.sell_ticket`</answer>
    <answer>`tkts.tickets_sold += 1`</answer>
    <answer>`BoxOffice.sell_ticket`</answer>
    <explanation>To increase the number of tickets sold for the `tkts` instance of the `BoxOffice` class, you just need to call the `sell_ticket` method on that instance.</explanation>
  </question>
</quiz>


<quiz>
  <question>
    <p>You are writing a program that makes sandwiches. Each sandwich has a protein, a condiment, and two slices of bread. There are different types of proteins, condiments, and breads, but within each of those categories, the different types are functionally all the same. According to the principles of Object-Oriented Programming, what classes should you create for your program?</p>
    <answer>Sandwich, Bread, RyeBread, SourDoughBread, WholeWheatBread, Protein, 
    Chicken, Tofu, Seitan, Turkey, Condiment, Mustard, Ketchup, Mayo</answer>
    <answer correct>Sandwich, Bread, Protein, Condiment</answer>
    <answer>Sandwich</answer>
    <answer>Sandwich, Bread, Protein, Mustard, Ketchup, Aioli</answer>
    <explanation>When taking an OOP approach, you typically want to break your program down into base classes (like `Bread`) that have a single responsibility / reason to change. If Sandwich were the only class, it would have to change whenever you needed to update the functionality of proteins, condiments, or bread, thus violating the preceding principle. At the same time, you don't need to break proteins, condiments, and bread down further because all of their different types share the same functionality.</explanation>
  </question>
</quiz>