## 1) Implement Stack ADT using Array

```
#include<stdio.h>
int stack[100],choice,n,top,x,i;
void push(void);
void pop(void);
void display(void);
int main()
{
//clrscr();
top=-1;
printf("\n Enter the size of STACK[MAX=100]:");
scanf("%d",&n);
printf("\n\t STACK OPERATIONS USING ARRAY");
printf("\n\t--------------------------------");
printf("\n\t 1.PUSH\n\t 2.POP\n\t 3.DISPLAY\n\t 4.EXIT");
do
{
printf("\n Enter the Choice:");
scanf("%d",&choice);
switch(choice)
{
case 1:
{
push();
break;
}
case 2:
{
pop();
break;
}
case 3:
{
display();
break;
}
case 4:
{
printf("\n\t EXIT POINT ");
break;
}
default:
{
printf ("\n\t Please Enter a Valid Choice(1/2/3/4)");
}
}
}
while(choice!=4);
return 0;
}
void push()
{
if(top>=n-1)
{
printf("\n\tSTACK is over flow");
}
else
{
printf(" Enter a value to be pushed:");
scanf("%d",&x);
top++;
stack[top]=x;
}
}
void pop()
{
if(top<=-1)
{
printf("\n\t Stack is under flow");
}
else
{
printf("\n\t The popped elements is %d",stack[top]);
top--;
}
}
void display()
{
if(top>=0)
{
printf("\n The elements in STACK \n");
for(i=top; i>=0; i--)
printf("\n%d",stack[i]);
printf("\n Press Next Choice");
}
else
{
printf("\n The STACK is empty");
}
}
```

## 2) Convert an Infix expression to postfix using stack adt

```
#include<stdio.h>
#include<ctype.h>
char stack[100];
int top = -1;
void push(char x)
{
stack[++top] = x;
}
char pop()
{
if(top == -1)
return -1;
else
return stack[top--];
}
int priority(char x)
{
if(x == '(')
return 0;
if(x == '+' || x == '-')
return 1;
if(x == '*' || x == '/')
return 2;
return 0;
}
int main()
{
char exp[100];
char *e, x;
printf("Enter the expression : ");
scanf("%s",exp);
printf("\n");
e = exp;
while(*e != '\0')
{
if(isalnum(*e))
printf("%c ",*e);
else if(*e == '(')
push(*e);
else if(*e == ')')
{
while((x = pop()) != '(')
printf("%c ", x);
}
else
{
while(priority(stack[top]) >= priority(*e))
printf("%c ",pop());
push(*e);
}
e++;
}
while(top != -1)
{
printf("%c ",pop());
}return 0;
}
```

## 3) Evaluate Postfix Expression using stack

```

#include <stdio.h>
#include <ctype.h>
#define MAXSTACK 100 /* for max size of stack */
#define POSTFIXSIZE 100 /* define max number of charcters in postfix expression */
/* declare stack and its top pointer to be used during postfix expression
evaluation*/

int stack[MAXSTACK];
int top = -1; /* because array index in C begins at 0 */
/* can be do this initialization somewhere else */

/* define push operation */
void push(int item)
{
if (top >= MAXSTACK - 1) 
{
printf("stack over flow");
return;
}
else 
{
top = top + 1;
stack[top] = item;
}
}

/* define pop operation */
int pop()
{
int item;
if (top < 0) {
printf("stack under flow");
}
else {
item = stack[top];
top = top - 1;
return item;
}
}

/* define function that is used to input postfix expression and to evaluate it */
void EvalPostfix(char postfix[])
{
int i;
char ch;
int val;
int A, B;
/* evaluate postfix expression */
for (i = 0; postfix[i] != ')'; i++) {
ch = postfix[i];
if (isdigit(ch)) {
/* we saw an operand,push the digit onto stack
ch - '0' is used for getting digit rather than ASCII code of digit */
push(ch - '0');
}
else if (ch == '+' || ch == '-' || ch == '*' || ch == '/') {
/* we saw an operator
* pop top element A and next-to-top elemnet B
* from stack and compute B operator A
*/
A = pop();
B = pop();
switch (ch) /* ch is an operator */
{
case '*':
val = B * A;
break;
case '/':
val = B / A;
break;
case '+':
val = B + A;
break;
case '-':
val = B - A;
break;
}
/* push the value obtained above onto the stack */
push(val);
}
}
printf(" \n Result of expression evaluation : %d \n", pop());
}

int main()
{
int i;
/* declare character array to store postfix expression */
char postfix[POSTFIXSIZE];
printf("ASSUMPTION: There are only four operators(*, /, +, -) in an expression and operand is
single digit only.\n");
printf(" \nEnter postfix expression,\npress right parenthesis ')' for end expression : ");
/* take input of postfix expression from user */
for (i = 0; i <= POSTFIXSIZE - 1; i++) {
scanf("%c", &postfix[i]);
if (postfix[i] == ')') /* is there any way to eliminate this if */
{
break;
} /* and break statement */
}
/* call function to evaluate postfix expression */
EvalPostfix(postfix);
return 0;
}
```

## 4) Implement Linear Queue ADT

```
#include<stdio.h>
#include<stdlib.h>
#define maxsize 5

void insert();
void delete();
void display();

int front = -1, rear = -1;
int queue[maxsize];

void main ()
{
int choice;
while(choice != 4)
{
printf("\n*************************Main Menu*****************************\n");
printf("\n=================================================================\n");
printf("\n1.insert an element\n2.Delete an element\n3.Display the queue\n4.Exit\n");
printf("\nEnter your choice ?");
scanf("%d",&choice);
switch(choice)
{
case 1: insert(); break;
case 2: delete(); break;
case 3: display(); break;
case 4: exit(0); break;
default: printf("\nEnter valid choice??\n");
}
}
}

void insert()
{
int item;
printf("\nEnter the element\n");
scanf("\n%d",&item);
if(rear == maxsize-1)
{
printf("\nOVERFLOW\n");
return;
}
if(front == -1 && rear == -1)
{
front = 0;
rear = 0;
}
else
{
rear = rear+1;
}
queue[rear] = item;
printf("\nValue inserted ");
}

void delete()
{
int item;
if (front == -1 || front > rear)
{
printf("\nUNDERFLOW\n");
return;
}
else
{
item = queue[front];
if(front == rear)
{
front = -1;
rear = -1 ;
}
else
{
printf("\nvalue deleted ");
}
}
}

void display()
{
int i;
if(rear == -1)
{
printf("\nEmpty queue\n");
}
else
{ printf("\nprinting values .....\n");
for(i=front;i<=rear;i++)
{
printf("\n%d\n",queue[i]);
}
}
}
```

## 5) Implement Circular Queue ADT

```

#include <stdio.h>
# define max 6
int queue[max]; // array declaration
int front=-1;
int rear=-1;
// function to insert an element in a circular queue
void enqueue(int element)
{
if(front==-1 && rear==-1) // condition to check queue is empty
{
front=0;
rear=0;
queue[rear]=element;
}
else if((rear+1)%max==front) // condition to check queue is full
{
printf("Queue is overflow..");
}
else
{
rear=(rear+1)%max; // rear is incremented
queue[rear]=element; // assigning a value to the queue at the rear position.
}
}

// function to delete the element from the queue
int dequeue()
{
if((front==-1) && (rear==-1)) // condition to check queue is empty
{
printf("\nQueue is underflow..");
}
else if(front==rear)
{
printf("\nThe dequeued element is %d", queue[front]);
front=-1;
rear=-1;
}
else
{
printf("\nThe dequeued element is %d", queue[front]);
front=(front+1)%max;
}
}

// function to display the elements of a queue
void display()
{
int i=front;
if(front==-1 && rear==-1)
{
printf("\n Queue is empty..");
}
else
{
printf("\nElements in a Queue are :");
while(i<=rear)
{
printf("%d,", queue[i]);
i=(i+1)%max;
}
}
}
int main()
{
int choice=1,x; // variables declaration
while(choice<4 && choice!=0) // while loop
{
printf("\n Press 1: Insert an element");
printf("\nPress 2: Delete an element");
printf("\nPress 3: Display the element");
printf("\nEnter your choice");
scanf("%d", &choice);
switch(choice)
{
case 1:
printf("Enter the element which is to be inserted");
scanf("%d", &x);
enqueue(x);
break;
case 2:
dequeue();
break;
case 3:
display();
}}
return 0;
}
```


## 6) Implement Priority Queue ADT

```
#include <stdio.h>
#include <stdlib.h>
#define MAX 10
void create_queue();
void insert_element(int);
void delete_element(int);
void check_priority(int);
void display_priorityqueue();
int pqueue[MAX];
int front, rear;
void main()
{
int n, choice;
printf("\nEnter 1 to insert element by priority ");
printf("\nEnter 2 to delete element by priority ");
printf("\nEnter 3 to display priority queue ");
printf("\nEnter 4 to exit");
create_queue();
while (1)
{
printf("\nEnter your choice : ");
scanf("%d", &choice);
switch(choice)
{
case 1: printf("\nEnter element to insert : ");
scanf("%d",&n);
insert_element(n);
break;
case 2: printf("\nEnter element to delete : ");
scanf("%d",&n);
delete_element(n);
break;
case 3: display_priorityqueue();
break;
case 4: exit(0);
default: printf("\n Please enter valid choice");
}
}
}

void create_queue()
{
front = rear = -1;
}
void insert_element(int data)
{
if (rear >= MAX - 1)
{
printf("\nQUEUE OVERFLOW");
return;
}
if ((front == -1) && (rear == -1))
{
front++;
rear++;
pqueue[rear] = data;
return;
}
else
check_priority(data);
rear++;
}
void check_priority(int data)
{
int i,j;
for (i = 0; i <= rear; i++)
{
if (data >= pqueue[i])
{
for (j = rear + 1; j > i; j--)
{
pqueue[j] = pqueue[j - 1];
}
pqueue[i] = data;
return;
}
}
pqueue[i] = data;
}

void delete_element(int data)
{
int i;
if ((front==-1) && (rear==-1))
{
printf("\nEmpty Queue");
return;
}
for (i = 0; i <= rear; i++)
{
if (data == pqueue[i])
{
for (; i < rear; i++)
{
pqueue[i] = pqueue[i + 1];
}
pqueue[i] = -99;
rear--;
if (rear == -1)
front = -1;
return;
}
}
printf("\n%d element not found in queue", data);
}
void display_priorityqueue()
{
if ((front == -1) && (rear == -1))
{
printf("\nEmpty Queue ");
return;
}
for (; front <= rear; front++)
{
printf(" %d ", pqueue[front]);
}
front = 0;
}

```


## 7) Implement Singly Linked List

```
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>

void insertAtBeginning(int);
void insertAtEnd(int);
void insertBetween(int,int,int);
void display();
void removeBeginning();
void removeEnd();
void removeSpecific(int);


struct Node
{
int data;
struct Node *next;
}*head = NULL;

void main()
{
int choice,value,choice1,loc1,loc2;
clrscr();

while(1){
mainMenu: printf("\n\n****** MENU ******\n1. Insert\n2. Display\n3. Delete\n4. Exit\nEnter your choice: ");
scanf("%d",&choice);

switch(choice)
{
case 1: printf("Enter the value to be insert: ");
scanf("%d",&value);
while(1){
printf("Where you want to insert: \n1. At Beginning\n2. At End\n3. Between\nEnter your ch
oice: ");
scanf("%d",&choice1);
switch(choice1)
{
case 1: insertAtBeginning(value);
break;
case 2: insertAtEnd(value);
break;
case 3: printf("Enter the two values where you wanto insert: ");
scanf("%d%d",&loc1,&loc2);
insertBetween(value,loc1,loc2);
break;
default: printf("\nWrong Input!! Try again!!!\n\n");
goto mainMenu;
}
goto subMenuEnd;
}
subMenuEnd:
break;
case 2: display();
break;
case 3: printf("How do you want to Delete: \n1. From Beginning\n2. From End\n3. Spesific\nEnter your choice:
");
scanf("%d",&choice1);
switch(choice1)
{
case 1: removeBeginning();
break;
case 2: removeEnd();
break;
case 3: printf("Enter the value which you wanto delete: ");
scanf("%d",&loc2);
removeSpecific(loc2);
break;
default: printf("\nWrong Input!! Try again!!!\n\n");
goto mainMenu;
}
break;
case 4: exit(0);
default: printf("\nWrong input!!! Try again!!\n\n");
}
}
}


void insertAtBeginning(int value)
{
struct Node *newNode;
newNode = (struct Node*)malloc(sizeof(struct Node));
newNode->data = value;
if(head == NULL)
{
newNode->next = NULL;
head = newNode;
}
else
{
newNode->next = head;
head = newNode;
}
printf("\nOne node inserted!!!\n");
}


void insertAtEnd(int value)
{
struct Node *newNode;
newNode = (struct Node*)malloc(sizeof(struct Node));
newNode->data = value;
newNode->next = NULL;
if(head == NULL)
head = newNode;
else
{
struct Node *temp = head;
while(temp->next != NULL)
temp = temp->next;
temp->next = newNode;
}
printf("\nOne node inserted!!!\n");
}

void insertBetween(int value, int loc1, int loc2)
{
struct Node *newNode;
newNode = (struct Node*)malloc(sizeof(struct Node));
newNode->data = value;
if(head == NULL)
{newNode->next = NULL;
head = newNode;
}
else
{
struct Node *temp = head;
while(temp->data != loc1 && temp->data != loc2)
temp = temp->next;
newNode->next = temp->next;
temp->next = newNode;
}
printf("\nOne node inserted!!!\n");
}

void removeBeginning()
{
if(head == NULL)
printf("\n\nList is Empty!!!");
else
{
struct Node *temp = head;
if(head->next == NULL)
{
head = NULL;
free(temp);
}
else
{
head = temp->next;
free(temp);
printf("\nOne node deleted!!!\n\n");
}
}
}

void removeEnd()
{
if(head == NULL)
{
printf("\nList is Empty!!!\n");
}
else
{
struct Node *temp1 = head,*temp2;
if(head->next == NULL)
head = NULL;
else
{
while(temp1->next != NULL)
{
temp2 = temp1;
temp1 = temp1->next;
}
temp2->next = NULL;
}
free(temp1);
printf("\nOne node deleted!!!\n\n");
}
}

void removeSpecific(int delValue)
{
struct Node *temp1 = head, *temp2;
while(temp1->data != delValue)
{
if(temp1 -> next == NULL){
printf("\nGiven node not found in the list!!!");
goto functionEnd;
}
temp2 = temp1;
temp1 = temp1 -> next;
}
temp2 -> next = temp1 -> next;
free(temp1);
printf("\nOne node deleted!!!\n\n");
functionEnd:
}

void display()
{
if(head == NULL)
{
printf("\nList is Empty\n");
}
else
{
struct Node *temp = head;
printf("\n\nList elements are - \n");
while(temp->next != NULL)
{
printf("%d --->",temp->data);
temp = temp->next;
}
printf("%d --->NULL",temp->data);
}
}
```


## 8) Implement Circular Linked List

```
 #include<stdio.h>
#include<conio.h>

void insertAtBeginning(int);
void insertAtEnd(int);
void insertAtAfter(int,int);
void deleteBeginning();
void deleteEnd();
void deleteSpecific(int);
void display();

struct Node
{
int data;
struct Node *next;
}*head = NULL;

void main()
{
int choice1, choice2, value, location;
clrscr();
while(1)
{
printf("\n*********** MENU *************\n");
printf("1. Insert\n2. Delete\n3. Display\n4. Exit\nEnter your choice: ");
scanf("%d",&choice1);
switch()
{
case 1: printf("Enter the value to be inserted: ");
scanf("%d",&value);
while(1)
{
printf("\nSelect from the following Inserting options\n");
printf("1. At Beginning\n2. At End\n3. After a Node\n4. Cancel\nEnter your choice: ");
scanf("%d",&choice2);
switch(choice2)
{
case 1: insertAtBeginning(value); break;
case 2: insertAtEnd(value); break;
case 3: printf("Enter the location after which you want to insert: ");
scanf("%d",&location);
insertAfter(value,location);
break;
case 4: goto EndSwitch;
default: printf("\nPlease select correct Inserting option!!!\n");
}
}

case 2: while(1)
{
printf("\nSelect from the following Deleting options\n");
printf("1. At Beginning\n2. At End\n3. Specific Node\n4. Cancel\nEnter your choice: ");
scanf("%d",&choice2);
switch(choice2)
{
case 1: deleteBeginning();
break;
case 2: deleteEnd();
break;
case 3: printf("Enter the Node value to be deleted: ");
scanf("%d",&location);
deleteSpecic(location);
break;
case 4: goto EndSwitch;
default: printf("\nPlease select correct Deleting option!!!\n");
}
}
EndSwitch: break;
case 3: display();
break;
case 4: exit(0);
default: printf("\nPlease select correct option!!!");
}
}
}

void insertAtBeginning(int value)
{
struct Node *newNode;
newNode = (struct Node*)malloc(sizeof(struct Node));
newNode -> data = value;
if(head == NULL)
{
head = newNode;
newNode -> next = head;
}
else
{
struct Node *temp = head;
while(temp -> next != head)
temp = temp -> next;
newNode -> next = head;
head = newNode;
temp -> next = head;
}
printf("\nInsertion success!!!");
}
void insertAtEnd(int value)
{
struct Node *newNode;
newNode = (struct Node*)malloc(sizeof(struct Node));
newNode -> data = value;
if(head == NULL)
{
head = newNode;
newNode -> next = head;
}
else
{
struct Node *temp = head;
while(temp -> next != head)
temp = temp -> next;
temp -> next = newNode;
newNode -> next = head;
}
printf("\nInsertion success!!!");
}
void insertAfter(int value, int location)
{
struct Node *newNode;
newNode = (struct Node*)malloc(sizeof(struct Node));
newNode -> data = value;
if(head == NULL)
{
head = newNode;
newNode -> next = head;
}
else
{
struct Node *temp = head;
while(temp -> data != location)
{
if(temp -> next == head)
{
printf("Given node is not found in the list!!!");
goto EndFunction;
}
else
{
temp = temp -> next;
}
}
newNode -> next = temp -> next;
temp -> next = newNode;
printf("\nInsertion success!!!");
}
EndFunction:
}
void deleteBeginning()
{
if(head == NULL)
printf("List is Empty!!! Deletion not possible!!!");
else
{
struct Node *temp = head;
if(temp -> next == head)
{
head = NULL;
free(temp);
}
else
{
head = head -> next;
free(temp);
}
printf("\nDeletion success!!!");
}
}
void deleteEnd()
{
if(head == NULL)
printf("List is Empty!!! Deletion not possible!!!");
else
{
struct Node *temp1 = head, temp2;
if(temp1 -> next == head)
{
head = NULL;
free(temp1);
}
else{
while(temp1 -> next != head){
temp2 = temp1;
temp1 = temp1 -> next;
}
temp2 -> next = head;
free(temp1);
}
printf("\nDeletion success!!!");
}
}
void deleteSpecific(int delValue)
{
if(head == NULL)
printf("List is Empty!!! Deletion not possible!!!");
else
{
struct Node *temp1 = head, temp2;
while(temp1 -> data != delValue)
{
if(temp1 -> next == head)
{
printf("\nGiven node is not found in the list!!!");
goto FuctionEnd;
}
else
{
temp2 = temp1;
temp1 = temp1 -> next;
}
}

if(temp1 -> next == head){
head = NULL;
free(temp1);
}
else{
if(temp1 == head)
{
temp2 = head;
while(temp2 -> next != head)
temp2 = temp2 -> next;
head = head -> next;
temp2 -> next = head;
free(temp1);
}
else
{
if(temp1 -> next == head)
{
temp2 -> next = head;
}
else
{
temp2 -> next = temp1 -> next;
}
free(temp1);
}
}
printf("\nDeletion success!!!");
}
FuctionEnd:
}
void display()
{
if(head == NULL)
printf("\nList is Empty!!!");
else
{
struct Node *temp = head;
printf("\nList elements are: \n");
while(temp -> next != head)
{
printf("%d ---> ",temp -> data);
}
printf("%d ---> %d", temp -> data, head -> data);
}
}
```

