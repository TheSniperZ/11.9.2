# 11.9.2
二叉树的遍历（含队列的实现）
// SY1807313_5.cpp : 定义控制台应用程序的入口点。
//

#include "stdafx.h"
#include<stdlib.h>
#include<iostream>
#include"Queue.h"
using namespace std;

struct Bitree*Create(void) {//按照前序遍历序列创建一个二叉树
	struct Bitree*q;//创建根节点
	q = (struct Bitree*)malloc(sizeof(struct Bitree));
	int x;
	cin >> x;
	q->date = x;
	if (x == 0) return NULL;
	cout << x << "->LiftTree= ";
	q->LiftTree = Create();
	cout << x << "->RightTree= ";
	q->RightTree = Create();
	return q;
}

void PreOrder(Bitree*root) {//前序遍历输出二叉树
	Bitree*p = root;
	if (p != NULL) {
		cout << p->date << "\t";
		PreOrder(p->LiftTree);
		PreOrder(p->RightTree);
	}
}
void InOrder(struct Bitree*root) {//中序遍历输出二叉树
	Bitree*p = root;
	if (p != NULL) {
		InOrder(p->LiftTree);
		cout << p->date << "\t";
		InOrder(p->RightTree);
	}
}
void PostOrder(struct Bitree*root) {//后序遍历输出二叉树
	Bitree*p = root;
	if (p != NULL) {
		PostOrder(p->LiftTree);
		PostOrder(p->RightTree);
		cout << p->date << "\t";
	}
}
void LevelOrder(struct Bitree*root) {//层次遍历输出二叉树
	Queue q;	
	q.Add(root);
	while (q.empty()!=true)
	{
		Bitree *cc=q.Del();
		cout << cc->date << "\t";
		if (cc->LiftTree != NULL) { q.Add(cc->LiftTree); }
		if (cc->RightTree !=NULL) { q.Add(cc->RightTree ); }
	}
}
int main()
{
	Bitree *Root;
	Root = Create();
	cout << "前序遍历结果为：";
	PreOrder(Root);
	cout <<endl<< "中序遍历结果为：";
	InOrder(Root);
	cout << endl << "后序遍历结果为：";
	PostOrder(Root);
	cout << endl << "层次遍历结果为：";
	LevelOrder(Root);
    return 0;
}

#pragma once
struct Bitree
{
	int date;
	struct Bitree*LiftTree;
	struct Bitree*RightTree;
};
class Queue
{
public:
	Queue();
	~Queue();
	void Add(Bitree*x);
	struct Bitree* Del();
	bool empty() const { //判断队列是否为空
		return count == 0;
	}
private:
	struct Que
	{
		struct Bitree* date;
		struct Que*next;
	};

	struct Que*front;//队头指针
	struct Que*rear;// 队尾指针
	int count=0;
};

#include "stdafx.h"
#include "Queue.h"
#include<stdlib.h>
#include <iostream>
using namespace std;
Queue::Queue()
{
	front = NULL;
	rear = NULL;
}


Queue::~Queue()
{
}

void Queue::Add(Bitree *x) {
	Que *p=new Que;
	p = (struct Que *)malloc(sizeof(struct Que));// 申请一个链结点 //
	p->date = x;
	if (count == 0) {
		front = rear =p;
		count++;
	}
	else
	{
		rear->next = p;
		rear = p;
		count++;
	}
}
struct Bitree* Queue::Del() {
	if (count != 0) {
		Que *p = front;
		Bitree* cc = p->date;
		front = front->next;
		count--;
		return cc;
	}
	else {
		cout << "队列为空！" << endl;
		return NULL;
	}
}
