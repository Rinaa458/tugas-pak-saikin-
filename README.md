class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class CircularLinkedList:
    def __init__(self):
        self.head = None

    def append(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            new_node.next = self.head
            return
        last = self.head
        while last.next != self.head:
            last = last.next
        last.next = new_node
        new_node.next = self.head

    def display(self):
        if not self.head:
            return
        current = self.head
        while True:
            print(current.data, end=" -> ")
            current = current.next
            if current == self.head:
                break
        print("(head)")

    def remove(self, key):
        if not self.head:
            return
        current = self.head
        previous = None
        while True:
            if current.data == key:
                if previous:
                    previous.next = current.next
                else:
                    if current.next == self.head:
                        self.head = None
                    else:
                        last = self.head
                        while last.next != self.head:
                            last = last.next
                        last.next = current.next
                        self.head = current.next
                return
            elif current.next == self.head:
                break
            previous = current
            current = current.next

# Example usage
cll = CircularLinkedList()
cll.append(1)
cll.append(2)
cll.append(3)
cll.display()  # Output: 1 -> 2 -> 3 -> (head)
cll.remove(2)
cll.display()  # Output: 1 -> 3 -> (head)
