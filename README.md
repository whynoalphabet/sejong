#pragma warning(disable:4996)
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int N=0;
typedef struct node{
    struct node *llink;
    char data;
    struct node *rlink;
}node;
node *getnode(char );
void add(node *,int, char);
void addnode(node *, char);
char get(node *,int);
void delete(node *,int);
void delnode(node *);
void print(node *);
int main() {
    node *head=NULL,*tail=NULL;
    head=getnode('1');
    tail=getnode('0');
    head->rlink=tail;
    tail->llink=head;//초기화
    int num,r;
    char type,e;
    scanf("%d",&num);
    getchar();
    for(int i=0;i<num;i++){
        scanf("%c",&type);
        getchar();
        if(type=='A'){
            scanf("%d %c",&r,&e);
            getchar();
            if(r<0||r>N+1){
                printf("invalid position\n");
                continue;
            }
            add(head, r, e);
        }
        if(type=='G'){
            scanf("%d",&r);
            getchar();
            if(r<0||r>N){
                printf("invalid position\n");
                continue;
            }
            printf("%c\n",get(head, r));
        }
        if(type=='D'){
            scanf("%d",&r);
            getchar();
            if(r<0||r>N){
                printf("invalid position\n");
                continue;
            }
            delete(head, r);
        }
        if(type=='P'){
            print(head);
            printf("\n");
        }
            
    }//for 끝
    printf("\n");
}
node *getnode(char e){
    node *new;
    new=(node *)malloc(sizeof(node));
    new->data=e;
    new->rlink=NULL;
    new->llink=NULL;
    return new;
}
void add(node *head,int r, char e){
    node *p;
    p=head;
    for(int i=0;i<r-1;i++){
        p=p->rlink;
    }
    addnode(p, e);
    N++;
}
void addnode(node *p, char e){
    node *q=getnode(e);
    q->rlink=p->rlink;
    (p->rlink)->llink=q;
    p->rlink=q;
    q->llink=p;
}
char get(node *head,int r){
    node *p=head;
    char result;
    for(int i=0;i<r;i++){
        p=p->rlink;
    }
    result=p->data;
    return result;
}
void delete(node *head,int r){
    node *p;
    p=head;
    for(int i=0;i<r;i++){
        p=p->rlink;
    }
    delnode(p);
    N--;
}
void delnode(node *p){
    (p->llink)->rlink=p->rlink;
    (p->rlink)->llink=p->llink;
}
void print(node *head){
    node *p=head;
    p=p->rlink;
    while(p->data!='0'){
        printf("%c",p->data);
        p=p->rlink;
    }
}
