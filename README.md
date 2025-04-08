1. Write a menu-driven program to implement the following operation on a single linked list: 
a. Creation 
b. Traversal 
c. Insertion at the beginning 
d. Insertion at the end 
e. Insertion at any location 
f. Delete the first node 
g. Delete the last node 
h. Deletion from any location 
i. Sorting 
j. Searching 
k. Reversing 
l. Merging

#include<stdio.h>
#include<stdlib.h>
struct node
{
	int data;
	struct node *next;
};
struct node *create_ll()
{
	int ch;
	struct node*head=NULL,*newnode,*temp;
	do
	{
		newnode=(struct node*)malloc(sizeof(struct node));
		printf("Enter Data\n");
		scanf("%d",&newnode->data);
		newnode->next=NULL;
		if(head==NULL)
		{
			head=newnode;
			temp=newnode;
		}
		else
		{
			temp->next=newnode;
			temp=temp->next;
		}
		printf("Enter\n 1.To create new node\n0.To Cancel\n");
		scanf("%d",&ch);
	}while(ch==1);
	return head;
}
int search(struct node *head,int x)
{
	struct node *temp=head;
	while(temp!=NULL)
	{
		if(temp->data==x)
		{
			return 1;
			temp=temp->next;
		}
		return 0;
	}
}
int len(struct node *temp)
{
	int c=0;
	while(temp!=NULL)
	{
		c=c+1;
		temp=temp->next;
	}
	return c;
}
void traverse(struct node *temp)
{
	while(temp!=NULL)
	{
		printf("%d\t",temp->data);
		temp=temp->next;
	}
	printf("\n");
}
struct node *insertl(struct node *head)
{
	struct node *newnode,*temp=head;
	while(temp->next!=NULL)
	{
		temp=temp->next;
	}
	newnode=(struct node*)malloc(sizeof(struct node));
	printf("Enter the data\n");
	scanf("%d",&newnode->data);
	newnode->next=NULL;
	temp->next=newnode;
	return head;
}
struct node *insertb(struct node *head)
{
	struct node *newnode;
	newnode=(struct node*)malloc(sizeof(struct node));
	if(newnode==NULL)
	{
		printf("Insertion not possible\n");
		return head;
	}
	printf("Enter the data\n");
	scanf("%d",&newnode->data);
	newnode->next=head;
	return newnode;
}
struct node *insert(struct node *head)
{
	struct node *newnode,*temp=head;
	int pos,t=1;
	printf("Enter the position\n");
	scanf("%d",&pos);
	if(pos>len(head))
	{
		printf("Not possible\n");
		return head;
	}
	while(t<pos-1)
	{
		temp=temp->next;
		t++;
	}
	newnode=(struct node*)malloc(sizeof(struct node));
	printf("Enter the data\n");
	scanf("%d",&newnode->data);
	newnode->next=temp->next;
	temp->next=newnode;
	return head;
}
struct node *deleteb(struct node *head)
{
	struct node *temp=head;
	head=head->next;
	free(temp);
	return head;
}
struct node *dtend(struct node *head)
{
	struct node *temp=head,*prev;
	while(temp->next!=NULL)
	{
		prev=temp;
		temp=temp->next;
	}
	if(head->next=NULL)
	{
		head=NULL;
	}
	else
	{
		prev->next=NULL;
		free(temp);
		return head;
	}
}
struct node *dtap(struct node *head)
{
	struct node *temp=head,*nextnode;
	int i,pos,l=len(head);
	printf("ENter the position to delete\n");
	scanf("%d",&pos);
	while(i<pos-2)
	{
		temp=temp->next;
		i++;
	}
	nextnode=temp->next;
	temp->next=nextnode->next;
	free(nextnode);
	return head;
}
struct node *merge(struct node *head1, struct node *head2)
{
	struct node *head=NULL,*tail,*newnode;
	while(head1!=NULL)
	{
		newnode=(struct node*)malloc(sizeof(struct node));
		newnode->data=head1->data;
		head1=head1->next;
		newnode->next=NULL;
		if(head==NULL)
		{
			head=newnode;
			tail=newnode;
		}
		else
		{
			tail->next=newnode;
			tail=tail->next;
		}
	}
	while(head2!=NULL)
	{
		newnode=(struct node*)malloc(sizeof(struct node));
		newnode->data=head2->data;
		head2=head2->next;
		newnode->next=NULL;
		if(head==NULL)
		{
			head=newnode;
			tail=newnode;
		}
		else
		{
			tail->next=newnode;
			tail=tail->next;
		}
	}
	return head;
}
struct node *reverse(struct node *head)
{
	struct node *curr=head,*prev=NULL,*next1;
	while(curr!=NULL)
	{
		next1=curr->next;
		curr->next=prev;
		prev=curr;
		curr=next1;
	}
	return prev;
}
struct node *swap(struct node*ptr1,struct node*ptr2)
{
	struct node *temp1=ptr2->next;
	ptr2->next=ptr1;
	ptr1->next=temp1;
	return ptr2;
}
struct node *sort(struct node *head)
{
	struct node *ptr1,*ptr2,**prev;
	int i,j,l=len(head);
	for(i=0;i<l;i++)
	{
		prev=&head;
		for(j=0;j<l-1-i;j++)
		{
			ptr1=*prev;
			ptr2=ptr1->next;
			if(ptr1->data>ptr2->data)
			{
				*prev=swap(ptr1,ptr2);
			}
			prev=&((*prev)->next);
		}
	}
	return *prev;
}
int main()
{
	struct node *head,*head1,*head2;
	int ch,x,c;
	head=create_ll();
	do
	{
		printf("ENter your choice\n1.INSERT AT BEGINNING\n2.INSERT AT LAST\n3.INSERT AT ANY POS\n4.DELETE AT BEGINING\n5.DELETE AT END\n6.DELETE ANY POS\n7.Traverse\n8.Search\n9.Merge\n10.Reverse\n11.Sort\n");
		scanf("%d",&ch);
		switch(ch)
		{
			case 1:
				head=insertb(head);
				break;
			case 2:
				head=insertl(head);
				break;
			case 3:
				head=insert(head);
				break;
			case 4:
				head=deleteb(head);
				break;
			case 5:
				head=dtend(head);
				break;
			case 6:
				head=dtap(head);
				break;
			case 7:
				traverse(head);
				break;
			case 8:
				printf("Enter the elemnt to search\n");
				scanf("%d",&x);
				c=search(head,x);
				if(c!=0)
					printf("ELement found\n");
				else
					printf("Not found\n");
				break;
			case 9:
				printf("Create a list\n");
				head1=create_ll();
				head=merge(head,head1);
				break;
			case 10:
				head=reverse(head);
				printf("Reverse list is\n");
				traverse(head);
				break;
			case 11:
				head=sort(head);
				printf("SOrted list is\n");
				traverse(head);
				break;
			case 0:
				printf("Exiting,,\n");
				break;
			default:
				printf("ENter valid choice\n");
		}
	}while(ch!=0);
	return 0;
}

	
