# Object-Oriented Domain Modeling in Java

Object-Oriented Domain Modeling in Java is a collection of three independent applications that translate real-world requirements into structured and maintainable software models. The work explores a pizzeria ordering system, a personal library with lending and sharing workflows, and a vehicle rental service. Each application demonstrates how domain entities, business rules, specialized behaviors, and exceptional conditions can be represented through clear object-oriented design, while executable scenarios show the collaboration between the different parts of each model.

## Overview

The repository contains three self-contained exercises. Each exercise includes its original assignment brief and a NetBeans-compatible Apache Ant project with an executable demonstration.

| Exercise | Domain | Main capabilities |
| --- | --- | --- |
| 01 | Pizzeria order management | Models pizzas and drinks for on-site and takeaway service, supports configurable products, calculates prices, associates deliveries or tables, and produces an order total. |
| 02 | Personal library management | Maintains mixed collections of paper books and ebooks, enforces book uniqueness, supports catalogue searches, manages paper-book loans, and limits ebook sharing. |
| 03 | Vehicle rental management | Represents multiple vehicle categories, calculates category-specific daily rates, maintains vehicle and rental collections, and associates rentals with customers and rental periods. |

The exercises are independent and do not share source code or runtime state. Their console applications create representative data and exercise the main domain operations from start to finish.

## Design Topics

The implementations focus on the following object-oriented programming concepts:

- abstraction through common base types for products, books, vehicles, and vans;
- inheritance to specialize shared state and behavior for concrete domain entities;
- interfaces to express capabilities such as pricing, service mode, lending, sharing, passenger capacity, and rental cost;
- polymorphism to manage heterogeneous objects through common contracts;
- enumerations to model closed sets of product options and vehicle categories;
- collection-based aggregates for orders, bookshelves, vehicle parks, and active rentals;
- value-based equality for catalogue integrity;
- checked exceptions for invalid or infeasible domain operations;
- date-based modeling for loans, vehicle registration, and rental periods.

## Exercise Details

### Exercise 01: Pizzeria Order Management

The first application models a pizzeria that serves customers on-site and through takeaway delivery. It distinguishes editable dine-in pizzas from fixed takeaway pizzas, represents draft and bottled drinks, applies flour and supplement pricing rules, and records either a table assignment or a delivery destination according to the selected service. The demonstration assembles dine-in and takeaway orders, changes an eligible pizza, calculates product prices, and produces a receipt total.

### Exercise 02: Personal Library Management

The second application models users who own collections containing both paper books and ebooks. The catalogue supports insertion, removal, and searches by title or author while preventing duplicate books. Paper books can be loaned to one user at a time with start and due dates, whereas ebooks can be shared within a fixed limit. The demonstration creates two users, populates their bookshelves, performs a loan, and records an ebook share.

### Exercise 03: Vehicle Rental Management

The third application models a rental fleet containing bicycles, motorcycles, cars, buses, and cargo vehicles. Vehicle types provide their own rental-rate calculations, while passenger-oriented types expose capacity information. Separate aggregates maintain the complete fleet and the rented vehicles. The demonstration creates a mixed fleet, registers a customer and rental period, calculates the total charge, and records the active rental.

## Prerequisites

Install the following tools before building the projects:

- Java Development Kit 17;
- Apache Ant 1.10 or later;
- a terminal capable of running PowerShell on Windows or a POSIX-compatible shell on macOS and Linux.

Confirm that the required executables are available:

```text
java -version
javac -version
ant -version
```

The first exercise targets Java 8 bytecode, while the second and third target Java 17. JDK 17 can build and run all three projects.

## Build and Run

Open a terminal in the repository root. Every project exposes the same Ant lifecycle:

- `ant clean` removes generated build outputs;
- `ant jar` compiles the source code and creates the executable JAR in the project's `dist` directory;
- `ant run` compiles the project when required and starts its console demonstration;
- `ant clean run` performs a clean build followed by execution.

### Windows

Run all exercises sequentially from PowerShell:

```powershell
$projects = @(
    "Exercise 01\exercise_01",
    "Exercise 02\exercise_02",
    "Exercise 03\exercise_03"
)

foreach ($project in $projects) {
    Push-Location $project
    try {
        ant clean run
    }
    finally {
        Pop-Location
    }
}
```

To run only one exercise, replace the path in the following example as needed:

```powershell
Set-Location "Exercise 01\exercise_01"
ant clean run
```

### macOS and Linux

Run all exercises sequentially from a POSIX-compatible shell:

```bash
for project in \
  "Exercise 01/exercise_01" \
  "Exercise 02/exercise_02" \
  "Exercise 03/exercise_03"
do
  (
    cd "$project" || exit 1
    ant clean run
  ) || exit 1
done
```

To run only one exercise, replace the path in the following example as needed:

```bash
cd "Exercise 01/exercise_01"
ant clean run
```

The console demonstrations do not require command-line arguments or interactive input.

## Running from NetBeans

Each inner exercise directory is an existing NetBeans Java project. Open the desired project directory in NetBeans, select JDK 17 as the Java platform, and use the IDE's Run Project action. The configured entry point for every exercise is `edu.unict.oop.Main`.

## Generated Outputs

Ant creates temporary compilation files in each project's `build` directory and the packaged application in its `dist` directory. Run `ant clean` from the corresponding project directory whenever these generated artifacts should be removed before a fresh build.
