#include<iostream>

using namespace std;

struct node
{
    int data;
    struct node *next;
};

struct node *first=NULL;

void append(int a)
{
    struct node *temp = new node;
    temp->data=a;
    temp->next=NULL;
    if (first==NULL)
    {
        first=temp;
    }
    else
    {
        struct node *p = first;
        while (p->next!=NULL)
        {
            p=p->next;
        }
        p->next=temp;
    }
}

void display()
{
    cout<<"\nList : ";
    if (first==NULL)
    {
        cout<<"\n\nList is empty\n";
    }
    else
    {
         struct node *te=first;
        while (te->next!=NULL)
        {
            cout<<te->data<<"\t";
            te=te->next;
        }
        cout<<te->data;
    }
}

void insertAtFirst(int a)
{
    struct node *temp=new node;
    temp->data=a;
    temp->next=first;
    first=temp;
}

struct node * findKey(int a)
{
    if (a==first->data)
    {
        return first;
    }
    struct node *temp=first;
    while (temp->next->data!=a)
    {
        temp=temp->next;
    }
    if (temp->next==NULL)
    {
        return NULL;
    }
    else
    {
        return temp;
    }
}

void insertAfterKey(struct node *p,int a)
{
    if (p==first)
    {
        struct node *te=new node;
        te->data=a;
        te->next=first->next;
        first->next=te;
    }
    else
    {
        p=p->next;
        struct node *temp=new node;
        struct node *t=p;
        temp->data=a;
        p=p->next;
        temp->next=p;
        t->next=temp;
    }
}

void insertBeforeKey(struct node *p,int a)
{
    struct node *temp=new node;
    temp->data=a;
    temp->next=p->next;
    p->next=temp;
}

void deleteKey(struct node *p)
{
    if (p==first)
    {
        first=first->next;
    }
    else
    {
        struct node *temp=p->next;
        p->next=p->next->next;
        temp->next=NULL;
    }
}

int main()
{
    int x,y;
    char c;
    MENU :
        cout<<"\n\n========== MENU : =============\n";
        cout<<"\n1. Append (at the rear)\n";
        cout<<"2. Insert at first\n";
        cout<<"3. Insert after a key element\n";
        cout<<"4. Insert before a key element\n";
        cout<<"5. Delete a key element\n";
        cout<<"6. Exit\n";
        cout<<"\n===============================\n";
    cout<<"Enter your choice : ";
    cin>>c;
    switch (c)
    {
    case '1' :
        cout<<"\nEnter the number : ";
        cin>>x;
        append(x);
        display();
        goto MENU;
        break;
    case '2' :
        cout<<"\nEnter the number : ";
        cin>>x;
        insertAtFirst(x);
        display();
        goto MENU;
        break;
    case '3' :
        cout<<"\nEnter the key element : ";
        cin>>x;
        if(findKey(x)==NULL)
        {
            cout<<"Key not found";
            goto MENU;
            break;
        }
        else
        {
            cout<<"Enter the number : ";
            cin>>y;
            insertAfterKey(findKey(x),y);
            display();
            goto MENU;
            break;
        }
    case '4' :
        cout<<"\nEnter the key element : ";
        cin>>x;
        if (x==first->data)
        {
            cout<<"Enter the number : ";
            cin>>y;
            insertAtFirst(y);
            display();
            goto MENU;
            break;
        }
        else if(findKey(x)==NULL)
        {
            cout<<"Key not found";
            goto MENU;
            break;
        }
        else
        {
            cout<<"Enter the number : ";
            cin>>y;
            insertBeforeKey(findKey(x),y);
            display();
            goto MENU;
            break;
        }
    case '5' :
        cout<<"\nEnter the key element : ";
        cin>>x;
        if (findKey(x)==NULL)
        {
            cout<<"Key not found";
            goto MENU;
            break;
        }
        else
        {
            deleteKey(findKey(x));
            display();
            goto MENU;
            break;
        }
    case '6' :
        break;
    default :
        cout<<"\nInvalid Choice";
        goto MENU;
    }
    return 0;
}
