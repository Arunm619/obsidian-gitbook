
1. Diagrams 
2. Go diagrams
3. Mermaid
4. PlantUML
5. ASCII Editor
6. Markmap


**Diagrams** 
- [Installation · Diagrams](https://diagrams.mingrammer.com/docs/getting-started/installation)
- Uses python 
- Renders images as output
```python diagram.py 
from diagrams import Diagram 
from diagrams.aws.compute import EC2 
from diagrams.aws.database import RDS 
from diagrams.aws.network import ELB 
with Diagram("Web Service", show=False): 
	ELB("lb") >> EC2("web") >> RDS("userdb")
```

**Go Diagrams** 
- Same as above except in Go language
- [GitHub - blushft/go-diagrams: Create beautiful system diagrams with Go](https://github.com/blushft/go-diagrams)
- Renders images as output
```go
go get github.com/blushft/go-diagrams 
```


**Mermaid**

- Generate diagrams from markdown-like text.
- Mermaid is a JavaScript-based diagramming and charting tool that uses Markdown-inspired text definitions and a renderer to create and modify complex diagrams. The main purpose of Mermaid is to help documentation catch up with development.
- Live editor - [Online FlowChart & Diagrams Editor - Mermaid Live Editor](https://mermaid.live/edit#pako:eNpVjstqw0AMRX9FaNVC_ANeFBq7zSbQQrPzZCFsOTMk80CWCcH2v3ccb1qtxD3nCk3Yxo6xxP4W760lUTjVJkCe96ay4gb1NJyhKN7mAyv4GPgxw_7lEGGwMSUXLq-bv18lqKbjqjGodeG6bKh69r8Cz1A3R0oa0_kvOd3jDB-N-7b5_H9ihXPrs-mp7KloSaAieSq4Q8_iyXX5_WlNDKplzwbLvHYkV4MmLNmjUePPI7RYqoy8wzF1pFw7ugj5LVx-AfLqVWg)
- Sample diagrams in the live editor is really cool
- Flow, Sequence, Class, State, ER, Gantt, User Journey, Git, Pie, XYChart, Block

**PlantUML**

- **PlantUML** is a versatile component that enables swift and straightforward diagram creation. Users can draft a variety of diagrams using a simple and intuitive language.
- [PlantUML Web Server](https://www.plantuml.com/plantuml/uml/SyfFKj2rKt3CoKnELR1Io4ZDoSa70000)
- Steeper learning curve 
- Solves more use cases
- Generate your diagrams in various formats including:
	- PNG
	- [SVG](https://plantuml.com/svg)
	- [LaTeX](https://plantuml.com/latex)
	- [ASCII art](https://plantuml.com/ascii-art)_(available only for sequence diagrams)_


**ASCII diagram editors**

- Tools allowing visual or text-based creation of diagrams rendered as ASCII art, leveraging the simplicity and versatility of plain text.
- [Text to ASCII Art Generator (TAAG)](https://patorjk.com/software/taag/#p=display&f=Graffiti&t=Type%20Something%20)
- [ASCII UML | ascii-uml.github.io](https://ascii-uml.github.io/)

MarkMap

- [markmap](https://markmap.js.org/)
- [Try markmap](https://markmap.js.org/repl)
- Visualizes mind maps from Markdown documents, useful for representing hierarchical relationships between ideas.



**Keywords**
- **Architectural diagrams**: Visual representations of system architectures.
- **Markdown**: A lightweight markup language for formatting plain text.
- **Prototyping**: Creating a preliminary version of a product for testing or demonstration.
- **Version control systems**: Software tools used to track and manage changes to code.
- **Domain-specific language**: A programming language specialized for a particular application domain.
- **ASCII art**: Artistic designs created using ASCII characters.
- **Hierarchies**: Systems or structures arranged in levels or ranks based on importance or function.
- **Documentation**: Information regarding how to use, deploy, or understand software systems.