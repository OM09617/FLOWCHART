from graphviz import Digraph

# Create the flowchart
dot = Digraph(format='png')
dot.attr(rankdir='TB', size='10')

# Nodes
dot.node('A', 'Start - Power ON (Battery → Regulator → +5V)', shape='box')
dot.node('B', 'Initialize ESP32, Sensors, LCD, RF', shape='box')
dot.node('C', 'Read Gas Sensors (CO, Methane, LPG)', shape='box')
dot.node('D', 'Read Temp & Humidity Sensor (DHT22)', shape='box')
dot.node('E', 'Update LCD with live values', shape='box')
dot.node('F', 'Any parameter above threshold?', shape='diamond')
dot.node('G1', 'YES → Activate Buzzer (Alert Mode)', shape='box')
dot.node('G2', 'NO → Continue Normal Operation', shape='box')
dot.node('H', 'Transmit data wirelessly via RF to PC/Laptop', shape='box')
dot.node('I', 'Monitoring Unit receives & logs data', shape='box')
dot.node('J', 'Loop back for continuous monitoring', shape='box')

# Edges
dot.edges([('A', 'B'), ('B', 'C'), ('C', 'D'), ('D', 'E'), ('E', 'F')])
dot.edge('F', 'G1', label='Yes')
dot.edge('F', 'G2', label='No')
dot.edge('G1', 'H')
dot.edge('G2', 'H')
dot.edge('H', 'I')
dot.edge('I', 'J')
dot.edge('J', 'A')

# Render the flowchart to a file
dot.render('gas_detection_flowchart', view=True)
