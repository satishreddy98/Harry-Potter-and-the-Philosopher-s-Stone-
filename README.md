# Harry-Potter-and-the-Philosopher-s-Stone
#include <math.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <assert.h>
#include <limits.h>
#include <stdbool.h>
typedef struct LinkedListNode LinkedListNode;
struct LinkedListNode {
    char val;
    LinkedListNode *next;
};
LinkedListNode* _insert_node_into_singlylinkedlist(LinkedListNode *head, LinkedListNode *tail, char val) {
    if(head == NULL) {
        head = (LinkedListNode *) (malloc(sizeof(LinkedListNode)));
        head->val = val;
        head->next = NULL;
        tail = head;
    }
    else {
        LinkedListNode *node = (LinkedListNode *) (malloc(sizeof(LinkedListNode)));
        node->val = val;
        node->next = NULL;
        tail->next = node;
        tail = tail->next;
    }
    return tail;
}
bool compare(LinkedListNode* a, LinkedListNode* b){
    while(a&&b){
        if(a->val!=b->val) return false;
        //printf("a = %c, b = %c\n",a->val,b->val);
        a = a->next;
        b = b->next;
    }
    return true;
}
LinkedListNode* rev(LinkedListNode *head){
    LinkedListNode* prev   = NULL, *current = head, *next = NULL;
    while (current != NULL)
    {
        next  = current->next;  
        current->next = prev;   
        prev = current;
        current = next;
    }
    return prev;
}
bool isPalindrome(LinkedListNode* head) {
    int len=0;
    LinkedListNode *t = head;
    while(t){
        len++;
        t = t->next;
    }
    LinkedListNode * a = head;
    LinkedListNode * b = head;
    int mid;
    if(len%2)
        mid = (len+1)/2;
    else 
        mid = len/2;
    while(mid--)
        b = b->next;
    b = rev(b);
    return compare(a,b);
}
int main()
{
    FILE *f = stdout;
    char *output_path = getenv("OUTPUT_PATH");
    if (output_path) {
        f = fopen(output_path, "w");
    }
    bool res;
    int head_size = 0;
    LinkedListNode* head = NULL;
    LinkedListNode* head_tail = NULL;
    scanf("%d", &head_size);
    char s[10005];
     scanf(" %s", s);
    for(int i = 0; i < head_size; i++) {
        char head_item = s[i];
        head_tail = _insert_node_into_singlylinkedlist(head, head_tail, head_item);

        if(i == 0) {
            head = head_tail;
        }
    }
    res = isPalindrome(head);
    fprintf(f, "%d\n", res);
    fclose(f);
    return 0;
}
