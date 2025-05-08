```cpp
Node* mergeTwoLists(Node* l1, Node* l2) {
    Node dummy(0); // Dummy node to simplify merging
    Node* curr = &dummy; // Pointer to build the merged list

    while (l1 != nullptr && l2 != nullptr) {
        if (l1->data < l2->data) {
            curr->next = l1; // Link current node from l1
            l1 = l1->next;   // Move to the next node in l1
        } else {
            curr->next = l2; // Link current node from l2
            l2 = l2->next;   // Move to the next node in l2
        }
        curr = curr->next; // Move curr to the last node in merged list
    }
    
    // Append remaining nodes
    curr->next = (l1 != nullptr) ? l1 : l2;

    return dummy.next; // Return the merged list, skipping the dummy node
}
			
`````