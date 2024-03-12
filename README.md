# Remove-Zero-Sum-Consecutive-Nodes-from-Linked-List
Given the head of a linked list, we repeatedly delete consecutive sequences of nodes that sum to 0 until there are no such sequences.  After doing so, return the head of the final linked list.  You may return any such answer.


class Solution:
    def removeZeroSumSublists(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prefixSum = 0
        mp = {}
        dummy = ListNode(0)
        dummy.next = head
        mp[0] = dummy
        while head:
            prefixSum += head.val
            if prefixSum in mp:
                start = mp[prefixSum]
                temp = start
                pSum = prefixSum
                while temp != head:
                    temp = temp.next
                    pSum += temp.val
                    if temp != head:
                        del mp[pSum]
                start.next = head.next
            else:
                mp[prefixSum] = head
            head = head.next
        return dummy.next
