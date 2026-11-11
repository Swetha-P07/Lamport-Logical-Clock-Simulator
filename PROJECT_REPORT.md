# Lamport Logical Clock Simulator — Project Notes

## 1. Problem Definition

In a distributed system, multiple processes execute independently and communicate by exchanging messages. Since there is no single global physical clock, determining the chronological order of events across processes is difficult.

This project simulates multiple distributed processes and assigns logical timestamps to internal, send, and receive events.

## 2. Objectives

- Create multiple independent distributed processes with separate logical clocks.
- Simulate internal, send, and receive events.
- Apply Lamport's logical clock update rules.
- Display event timestamps and a consistent logical ordering.
- Demonstrate that a receive event is ordered after its corresponding send event.

## 3. System Architecture

The simulator contains three process clocks (P1, P2, and P3), an event generator, a message-passing mechanism, and an event-ordering view. Each process maintains its own logical clock.

Conceptual flow:

`Process → Event → Logical Clock Update → Message (if any) → Receiving Process → Clock Update → Event List → Logical Ordering`

## 4. Algorithm

1. Initialize every process clock to zero.
2. For an internal event, increment the local clock by one.
3. For a send event, increment the sender clock and attach the timestamp to the message.
4. For a receive event carrying timestamp T, set the receiver clock to `max(local clock, T) + 1`.
5. Store each event with its process, event type, details, and timestamp.
6. Sort the display list by timestamp, then process ID as a deterministic tie-breaker.

## 5. Test Scenarios

| Test | Scenario | Expected result |
|---|---|---|
| TC01 | One internal event at P1 | P1 clock becomes 1 |
| TC02 | P1 sends a message to P2 | P1 send timestamp increments |
| TC03 | P2 receives a message with timestamp 2 | P2 receive clock becomes `max(0, 2) + 1 = 3` |
| TC04 | P3 sends a message to P1 | P3 send timestamp increments |
| TC05 | P3 receives a message with timestamp 5 while its clock is 3 | P3 becomes `max(3, 5) + 1 = 6` |
| TC06 | Independent events have equal timestamps | Equal logical times are permitted |

## 6. Results and Discussion

The simulator demonstrates that each process can maintain an independent logical clock. Message communication transfers causal information from the sender to the receiver. When a receive event occurs, the receiver advances its clock beyond the message timestamp.

Events on different processes may have equal Lamport timestamps. This does not mean that one caused the other.

## 7. Conclusion

The project demonstrates internal events, message sending, message receiving, logical timestamp updates, and event ordering. If event A happened before event B, Lamport timestamps satisfy `timestamp(A) < timestamp(B)`.

## References

- Leslie Lamport, “Time, Clocks, and the Ordering of Events in a Distributed System,” *Communications of the ACM*, 1978.
- Andrew S. Tanenbaum and Maarten Van Steen, *Distributed Systems: Principles and Paradigms*.
- George Coulouris, Jean Dollimore, Tim Kindberg and Gordon Blair, *Distributed Systems: Concepts and Design*.
