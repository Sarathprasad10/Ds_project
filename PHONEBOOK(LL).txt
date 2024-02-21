#include<stdio.h>
#include<stdlib.h>
#include<string.h>
struct node
{
    char name[100];
    char pnum[100];
    struct node *next;
};
struct node *head=NULL;
void insert(char*uname,char*pn) //function to insert values
{ 	
	int flag=0;
    struct node*t;
    if(head==NULL)
    {
        head=(struct node*)malloc(sizeof(struct node));
        strcpy(head->name,uname);
        strcpy(head->pnum,pn);
        head->next=NULL;
        printf("\nNew contact added successfully");
    }
    else
    {
    	t=head;
    	while(t->next!=NULL)
    	{
    		if(strcmp(t->name,uname)==0)
    		{
    			flag=1;
    			break;
			}
			t=t->next;	
    	}
			if(flag==0&&(strcmp(t->name,uname)!=0))
    		{ 
        		t=head;
        		while(t->next!=NULL&&strcmp(t->name,uname)!=0)
        		{
            		t=t->next;
        		}
        		t->next=(struct node*)malloc(sizeof(struct node));
        		strcpy(t->next->name,uname);
        		strcpy(t->next->pnum,pn);
        		t->next->next=NULL;
        		printf("\nNew contact added successfully");
    		}
            else
        	{
    		    printf("\nName is already taken");
		    }
	    }
}
void display() //function to display phone-book
{   int i=1;
        struct node*t;
        if(head==NULL)
        {
                printf("\nNO CONTACTS FOUND");
        }
        else
        {   
            
            printf("             CONTACTS\n");
            printf("----------------------------------------------\n");
            printf("NO.  |NAME\t\t  |NUMBER \t  |");
            printf("\n----------------------------------------------");
            t=head;
            while(t!=NULL)
            {
                printf("\n%-5d|%-20s|%-15s|",i,t->name,t->pnum);
                        t=t->next;
                i++;
            }
        }
}
void search(char*sname)  //function to search contact
{
        int flag=0;
        struct node*t;
        t=head;
        while(t!=NULL)
        {
                if(strcmp(t->name,sname)==0)
                {
                    printf("\n             CONTACT FOUND\n");
                    printf("----------------------------------------------\n");
                    printf("|NAME\t\t     |NUMBER \t     |");
                    printf("\n----------------------------------------------");  
                    printf("\n|%-20s|%-15s|",t->name,t->pnum);
                    flag=1;
                   
                }
                t=t->next;
        }
        if(flag==0)
        {
            printf("\nCONTACT NOT FOUND :(");
        }
                
}
void delete(char*dname) //function to delete the contacts
{
    struct node*t;
    if(head==NULL)
    {
        printf("\nPHONE-BOOK IS EMPTY");
    }
    else if((strcmp(head->name,dname)==0)&&head->next==NULL)
    {
        printf("\n %s s'Contact  has been deleted ",dname);
            head=NULL;
    }
    else if((strcmp(head->name,dname)==0)&&head->next!=NULL)
    {
        printf("\n %s s'Contact  has been deleted ",dname);
        head=head->next;
    }
    else
    {       t=head;
            while((strcmp(t->next->name,dname)!=0)&&t->next->next!=NULL)
            {
                    t=t->next;
            }
            if(strcmp(t->next->name,dname)==0)
            {
                    printf("\n %s s'Contact  has been deleted ", dname);
                    t->next=t->next->next;
            }
            else
            {
                  printf("\nCONTACT NOT FOUND");
            }
    }
}
int update_name()   //function to update the name of contact
{
    char sn[100],uname[100];
    struct node*t;
    t=head;
    int flag=0;
    printf("\nEnter the name to be updated: ");
    scanf("%s", sn);
    flag = 0; 
    while (t != NULL) 
    {
        if (strcmp(t->name, sn) == 0) 
        {
            printf("Enter the new name: ");
            scanf("%s", uname);
            struct node *temp = head;
            while (temp != NULL) 
            {
                if (strcmp(temp->name, uname) == 0) 
                {
                    printf("\nThis name is already taken.");
                    flag = 1;
                    break;
                }
                temp = temp->next;
            }
            if (flag == 0) 
            {
                strcpy(t->name, uname);
                printf("\nName updated successfully.");
                return 1;
            }
        }
        t = t->next;
    }
    if (flag == 0) 
    {
        printf("Name not found in the contacts.");
    }
    return -1;
}
int update_number() //function to  update the phone number
{
    int flag=0;
    char sn[100],upno[100];
    struct node*t;
    t=head;
    printf("\nEnter the name associated with the phone number to be updated:");
                scanf("%s", sn);
                while(t!=NULL)
                {
                    if(strcmp(t->name,sn)==0)
                    {
                            printf("Enter the new number");
                            scanf("%s",upno);
                            strcpy(t->pnum,upno);
                            flag=1;
                            break;
                          
                    }
                    t=t->next;
                }
                
                if(flag==1)
                {
                         printf("Phone number updated successfully.");
                         
                }
                else
                {
                     printf("CONTACT NOT FOUND");
                     return 0;
                }
                  
                
}
void update()
{
    int m;
    printf("\n1.UPDATE NAME:");
    printf("\n2.UPDATE PHONE NUMBER:");
    printf("\n3.BACK TO THE MENU");
    printf("\nEnter your choice:");
    scanf("%d", &m);
    if(head!=NULL)
    {
        switch (m) 
        {
            case 1:update_name();
            break;
                
            case 2:update_number();
                break;
            case 3:printf("BACK\n");
                 break;
            default:printf("\nWrong choice");
                break;
        }
    }
    else
    {
        printf("\nPHONE-BOOK IS EMPTY");
    }
   
}

int main()
{
    int ch;
    char n[100],pno[100],s[100],d[100];
    printf("\t\t---------------------\n");  
    printf("\t\t\t PHONE-BOOK      ");
    printf("\n\t\t\t---------------------");  
    printf("\n\t\t\t|1.INSERT  |");
    printf("\n\t\t\t|2.DISPLAY |");
    printf("\n\t\t\t|3.SEARCH  |");
    printf("\n\t\t\t|4.DELETE  |");
    printf("\n\t\t\t|5.UPDATE  |");
    printf("\n\t\t\t|6.EXIT    |");
    do{    
       printf("\nENTER YOUR CHOICE:");
       scanf("%d",&ch);
        switch(ch)
         {
            case 1:printf("\nEnter the name:");
                    scanf("%s",n);
                    printf("\nEnter the phone number:");
                    scanf("%s",pno);
                    insert(n,pno);
                    break;
            case 2:printf("\n");
                    display();
                    break;
            case 3:printf("Enter the name to search for:");
                    scanf("%s",s);
                    search(s);
                    break;
            case 4:printf("Enter the name of the contact you want to delete:");
                    scanf("%s",d);
                    delete(d);
                    break;
            case 5:update();
                    break;
            case 6:printf("\n**EXIT**");
                    break;
            default:printf("\nWRONG CHOICE");
                    break;
        }
                
    }while(ch!=6);
        
}