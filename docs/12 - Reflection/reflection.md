# Reflection

## Review of Module’s Success

This project successfully achieved several of the core goals of the module. The team developed a complete hardware and software design, documented the system thoroughly, and produced a final prototype that demonstrated the intended project direction. The block diagram, component selection, schematic, PCB, BOM, and API documentation all show the design process from concept to implementation.

Even though the final system did not work perfectly, the project still succeeded in showing how the hardware and software were intended to function together. The final documentation also captures the major design decisions made during development. Some parts of the design required compromises, especially in the power regulation section and the ESP32 integration, but those issues helped reveal important lessons about hardware validation, debugging, and layout decisions.

## Microcontroller / Module Startup Tips

One of the most helpful things learned during the project was to verify the basic hardware first before trying to debug the whole system at once. Power, grounding, programming access, and communication lines should all be checked early, because a single small mistake in those areas can prevent the entire system from working.

Another useful tip is to test each subsystem separately. It is much easier to debug a regulator, a microcontroller, or a connector by itself than it is to troubleshoot everything at once. It also helps to confirm that the PCB layout matches the schematic before assembly, since even small placement mistakes can create major problems later.

A third important lesson was to pay attention to physical access to connectors. The micro USB connection on this project was difficult to use because it was not placed near the PCB edge. That made the board harder to program and test. This showed how important mechanical layout is, not just electrical correctness.

## Lessons Learned

The first major lesson learned from this project was that careful planning matters at every stage of hardware development. A design can look correct on paper and still fail if the details of grounding, component selection, or placement are not handled correctly. This project showed that the schematic, PCB layout, and assembly choices all need to work together for the full system to function.

The second lesson was that debugging hardware takes time and patience. The power regulator issue and the ESP32 problem both required repeated testing, but neither issue could be solved quickly. That made it clear that good debugging depends on breaking the system into smaller parts and checking one section at a time. It is much easier to find the source of a problem when each block is tested individually.

The third lesson was that component choice affects more than electrical performance. Some components were difficult to solder or access, especially parts that should have been easier to connect during assembly. In future designs, choosing through hole components for certain connections, such as ribbon cable headers, would improve reliability and make assembly easier.

The fourth lesson was that PCB layout has a major effect on usability. Even when the board is technically correct, poor connector placement can make the system frustrating to use. The micro USB port issue showed that access, orientation, and board edge placement are important design decisions, not afterthoughts.

The fifth lesson was that documentation is valuable because it forces the design decisions to be clear. Writing the report and updating the datasheet made it easier to identify what worked, what did not work, and what should be changed in a future version. Good documentation also makes it easier for other people to understand the project without needing extra explanation.

The sixth lesson was that testing should begin as early as possible. Waiting until the full board is assembled before checking major assumptions can make problems harder to isolate. Verifying critical pieces like the regulator and the microcontroller early would have saved time later in the process.

The seventh lesson was that a successful project is not only about making something work once. It is also about building something that is repeatable, understandable, and easier to troubleshoot next time. This project helped show the difference between a rough prototype and a more polished engineering design.

The eighth lesson was that communication between hardware and software is just as important as either one alone. Even if the circuit is built correctly, the system still will not function if the microcontroller setup or interface is incorrect. That made it clear that both sides of the design must be checked together.

The ninth lesson was that design changes should be made with the full system in mind. A small change in placement or part selection can affect soldering, debugging, or even whether the board can be used at all. Future designs should treat those details as part of the main engineering problem.

The tenth lesson was that persistence is a real part of engineering. Not every issue had a clean answer, and some problems remained unresolved by the end of the project. Even so, working through those issues improved problem solving skills and made the design process more realistic.

## Recommendations for Future Students

1. Start the project early and do not wait until the end to begin debugging, because hardware problems often take longer than expected to solve.
2. Test the power system and microcontroller separately before assembling the full design, since those are common sources of failure.
3. Keep the PCB layout practical by placing connectors where they can actually be accessed and used during programming and testing.
4. Choose components carefully and consider whether through hole parts would make assembly and debugging easier in certain places.
5. Write down every design change and problem as the project goes on, because good notes make the final report and troubleshooting much easier.
