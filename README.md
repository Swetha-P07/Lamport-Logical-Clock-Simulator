# Lamport Logical Clock Simulator

A browser-based mini project that demonstrates Lamport logical clocks in a distributed system with three independent processes: **P1, P2, and P3**.

## Features

- Independent logical clocks for P1, P2, and P3
- Internal event simulation
- Message sending between processes
- Message receiving with Lamport timestamp updates
- Execution-order event log
- Consistent logical ordering by timestamp and process ID
- Sample demonstration and reset controls
- Responsive interface for desktop and mobile

## Run the project

This is a static web project. No Python, Java, Node.js, database, or server is required.

1. Download or clone this repository.
2. Open `index.html` in any modern web browser.
3. Select a process and event type.
4. Add internal, send, and receive events.
5. View the event log and sorted logical ordering.

You can also publish it with **GitHub Pages**:
1. Push the repository to GitHub.
2. Open the repository's **Settings → Pages**.
3. Choose **Deploy from a branch**.
4. Select the `main` branch and `/ (root)`.
5. Save and open the generated Pages URL.

## Lamport clock rules

1. Every process starts with clock value `0`.
2. Internal event: `clock = clock + 1`.
3. Send event: increment the sender clock and attach its value to the message.
4. Receive event: `clock = max(local clock, received timestamp) + 1`.
5. Events are displayed in timestamp order. Process ID is used only as a deterministic tie-breaker.

## Sample demonstration

Use **Load Sample Demonstration** to generate the sample sequence from the project report. It creates ten events across P1, P2, and P3 and shows their timestamps and sorted ordering.

## Project structure

```text
lamport-logical-clock-simulator/
├── index.html
├── README.md
├── LICENSE
├── .gitignore
└── docs/
    └── PROJECT_REPORT.md
```

## Technology

- HTML5
- CSS3
- Vanilla JavaScript

## Academic note

Equal Lamport timestamps do not imply that two events are causally related. Lamport clocks provide an ordering that respects the happened-before relation; they do not fully identify all concurrent events.
