# prim
备份
// primeandkruskal.cpp : 定义控制台应用程序的入口点。
//

#include "stdafx.h"

#include<iostream>
#include<string>
#include <vector>
#include <queue>
using namespace std;
//template <class T>
struct GraphNode//图结点
{
	string  vertexName; //顶点名称
	bool visited;  //访问标记
	float weight; //顶点权值
	int index;  //顶点标号
	friend bool operator<(GraphNode a, GraphNode b) //自定义优先级，weight 小的优先
	{
		return a.weight > b.weight;
	}
};
template <class T>
class Graph
{
public:
	//********************邻接矩阵函数************************************//
	Graph(int* vertexArray, T* nameOfVertex, int numberOfVertex);//构造函数，初始化具有 n个顶点的图
		//~Graph();//析构函数
	void Prim(int source);//Prim 算法
	void GetVexInfo();//取顶点信息
	void GetArcInfo();//输出变信息
	void SetArc(int vertextFrom, int vertextTo, int arcLength);//修改边
	void DeleteVex(int vertex);//删除顶点 vertex
	void InsertVex(int position, T name);//在 position 的位置上插入一顶点，值为 name
	void DeleteArc(int vertextFrom, int vertextTo);//在图中删除一条边，其依附的两个顶点的编号为 vertextFrom 和 vertextTo
		void InsertArc(int vertextFrom, int vertextTo, int value);//在图中插入一条边，其依附的两个顶点的编号为 vertextFrom 和 vertextTo
		void PrintAdjacencyMatrix();//输出邻接矩阵
private:
	int vertexNum, arcNum;//图的顶点数和边数
						  //vector<T> vertexName;//存放图中顶点的数组
	vector< vector<int> > adjacencyMatrix;//邻接矩阵 adjacencyMatrix
	vector< GraphNode > graphNodeArray;//存放图中顶点的数组
};
template <class T>
Graph<T>::Graph(int* vertexArray, T* nameOfVertex, int numberOfVertex)//构造图
{
	vertexNum = numberOfVertex;//顶点数
	arcNum = 0;//边数
	GraphNode tempGraphNode;
	for (int i = 0; i < vertexNum; i++)
	{
		tempGraphNode.vertexName = nameOfVertex[i];
		tempGraphNode.index = i;
		graphNodeArray.push_back(tempGraphNode);
	}
	adjacencyMatrix.resize(vertexNum, vector<int>(vertexNum));
	for (int i = 0; i < vertexNum; i++)//给边赋置
		for (int j = 0; j < vertexNum; j++)
		{
			adjacencyMatrix[i][j] = *(vertexArray + i*vertexNum + j);
			if (adjacencyMatrix[i][j] < INT_MAX)
				arcNum++;
		}
	this->arcNum = arcNum / 2;//无向图
}
template <class T>
void Graph<T>::PrintAdjacencyMatrix()
{
	cout << "图 G 的顶点数是:" << vertexNum << endl;//输出顶点数
	cout << "顶点向量的值是:" << endl;
	for (int i = 0; i < graphNodeArray.size(); i++)
		cout << graphNodeArray[i].vertexName << endl;//输出顶点表各顶点数据
	cout << "图 G 的边数是:" << arcNum << endl; //输出边数
	for (int i = 0; i < adjacencyMatrix.size(); i++)
		for (int j = i + 1; j < adjacencyMatrix.size(); j++) {
			if (adjacencyMatrix[i][j] < INT_MAX) //有效，输出边
				cout << "(" << i << ", " << j << ", " << adjacencyMatrix[i][j] << ")" << endl;
		}
}
/*
前置条件：图已存在
输入：无
功能：输出图中所有顶点的数据信息
输出：图中所有顶点的数据信息
后置条件：图保持不变
*/
template <class T>
void Graph<T>::GetVexInfo()//取顶点
{
	for (int i = 0; i < graphNodeArray.size(); i++)//输出图中所有的顶点
	{
		cout << graphNodeArray[i].vertexName << "\n";
	}
}
/* 前置条件：图已存在
输入：顶点 v1,v2
功能：修改顶点 v1、v2 的路径
输出：修改后图中所有的路径
后置条件：图保持不变
*/
template <class T>
void Graph<T>::SetArc(int vertextFrom, int vertextTo, int arclength)//修改路径
{ //假设源点是第 0 个顶点，即顶点序号是 0
	if (vertextFrom > vertexNum || vertextTo > vertexNum) throw "位置";//错误抛出异常
	else
	{
		adjacencyMatrix[vertextFrom][vertextTo] = arclength; //修改 v1 顶点到 v2 顶点的距离
		adjacencyMatrix[vertextTo][vertextFrom] = arclength;
	}
}
/*
前置条件：图已存在
输入：无
功能：输出图中所有的路径
输出：图中所有顶点的数据信息
后置条件：图保持不变
*/
template <class T>
void Graph<T>::GetArcInfo()//获取图中边的信息
{
	for (int i = 0; i < graphNodeArray.size(); i++)
	{//输出任意两点之间的路径
		for (int j = 0; j < i; j++)
		{
			if (adjacencyMatrix[i][j] < INT_MAX)//两点之间存在路径
											  //若两点间有路，则输出该两点间的路径
				cout << " 从 " << graphNodeArray[i].vertexName << " 到 " <<
				graphNodeArray[j].vertexName
				<< "的路径长度为：" << adjacencyMatrix[i][j] << "\n";
		}
	}
}
/*
前置条件：图已存在
输入：顶点 name,位置 i
功能：在图中 i 位置插入一个顶点 name
输出：如果插入不成功，抛出异常
后置条件：如果插入成功，图中增加了一个顶点
*/
template <class T>
void Graph<T>::InsertVex(int position, T name)//在图中插入一个顶点，其插入位置为 position，顶点名称为 name
{ //假设源点是第 0 个顶点，即顶点序号是 0
	if (position<0 || position>graphNodeArray.size()) throw "位置不正确";//如果 num 输入不正确抛出异常
	vector<int>tempRow(graphNodeArray.size(), INT_MAX);
	GraphNode tempGraphNode;
	tempGraphNode.vertexName = name;
	graphNodeArray.insert(graphNodeArray.begin() + position, tempGraphNode);
	adjacencyMatrix.insert(adjacencyMatrix.begin() + position, tempRow);
	for (unsigned i = 0; i < graphNodeArray.size(); ++i)
	{
		adjacencyMatrix[i].insert(adjacencyMatrix[i].begin() + position, INT_MAX);
	}
	this->vertexNum = this->vertexNum + 1;
}
/*
前置条件：图已存在
输入：顶点 pos
功能：在图中删除顶点 pos
输出：如果删除不成功，抛出异常
后置条件：如果删除成功，图中减少了一个顶点,相应顶点所建立的边也消去
*/
template <class T>
void Graph<T>::DeleteVex(int position)//删除 vertex 顶点
{ //假设源点是第 0 个顶点，即顶点序号是 0
	if (position<0 || position>adjacencyMatrix.size()) throw "位置";//如果 postion 输入不正确抛出异常
		int vertexNum = adjacencyMatrix.size();//vertexNum 等于顶点数
	if (position > -1)//postion 存在
	{
		graphNodeArray.erase(graphNodeArray.begin() + position);
		//verIndex.erase(verIndex.begin() + postion);
		//删除行
		if (adjacencyMatrix.size() > position)
		{
			adjacencyMatrix.erase(adjacencyMatrix.begin() + position);
		}
		//删除列
		for (unsigned i = 0; i < adjacencyMatrix.size(); ++i)
		{
			if (adjacencyMatrix[i].size() > position)
			{
				if (adjacencyMatrix[i][position] != INT_MAX)
				{
					this->arcNum = this->arcNum - 1;
				}
				adjacencyMatrix[i].erase(adjacencyMatrix[i].begin() + position);
			}
		}
		this->vertexNum = this->vertexNum - 1;
	}
}
/*
前置条件：图已存在
输入：顶点 n、w
功能：在图中删除顶点 n、w 依附的边
输出：如果删除不成功，抛出异常
后置条件：如果删除成功，图中减少了一条边
*/
template <class T>
void Graph<T>::DeleteArc(int vertextFrom, int vertextTo)//删除vertextFrom与vertextTo两顶点依附的边
{
	if (vertextFrom > vertexNum || vertextTo > vertexNum) throw "位置";//如果输入不正确抛出异常
		//将 vertextFrom 与 vertextTo 两顶点依附的边设置为无穷大
		adjacencyMatrix[vertextFrom][vertextTo] =
		adjacencyMatrix[vertextTo][vertextFrom] = INT_MAX;
	this->arcNum = this->arcNum - 1;
}
/* 前置条件：图已存在
输入：顶点 i、j
功能：在图中插入顶点 i、j 及其所依附的边
输出：如果插入不成功，抛出异常
后置条件：如果插入成功，图中增加了一条边
*/
template <class T>
void Graph<T>::InsertArc(int vertextFrom, int vertextTo, int value)//在图中插入一条边，其依附的两个顶点的编号为 vertextFrom 和 vertextTo
{
	if (vertextFrom > vertexNum || vertextTo > vertexNum) throw "位置";//如果输入不正确抛出异常
	if (adjacencyMatrix[vertextFrom][vertextTo] == INT_MAX)
	{
		adjacencyMatrix[vertextFrom][vertextTo] = value;
		adjacencyMatrix[vertextTo][vertextFrom] = value;
		//输出所插入的两个顶点之间的距离
		cout << " 从 " << graphNodeArray[vertextFrom].vertexName << " 到 " <<
			graphNodeArray[vertextTo].vertexName
			<< "的路径长度为：" << adjacencyMatrix[vertextFrom][vertextTo] << "\n";
		this->arcNum = this->arcNum + 1;
	}
	else
		cout << "边已经存在！" << endl;
}
/*
前置条件：图已存在
输入：顶点 v ，endv
功能：假如 endv 存在，求 v 到 endv 的最短路径；假如不输入 endv，则求 v 到任意顶点的
最短路径
输出：所求得的最短路径及所经历的位置
后置条件：图保持不变
*/
template <class T>
void Graph<T>::Prim(int source)//最小生成树
{
	int i, j, k, tk, tj;
	for (i = 0; i < graphNodeArray.size(); i++)
		graphNodeArray[i].visited = 0;
	graphNodeArray[source].visited = 1;
	for (i = 0; i < graphNodeArray.size() - 1; i++)
	{
		for (j = 0, tj = 0, tk = 0; j < graphNodeArray.size(); j++)
		{
			for (k = j + 1; k < graphNodeArray.size(); k++)
			{
				if ((graphNodeArray[j].visited == 0 && graphNodeArray[k].visited == 1) || (graphNodeArray[k].visited == 0 && graphNodeArray[j].visited == 1))
					if (adjacencyMatrix[j][k] < adjacencyMatrix[tj][tk])
					{
						tj = j;
						tk = k;
					}
			}
		}
		cout << graphNodeArray[tj].vertexName << " --->" << graphNodeArray[tk].vertexName << "\t";
		if (graphNodeArray[tk].visited == 0)
			graphNodeArray[tk].visited = 1;
		else if (graphNodeArray[tj].visited == 0)
			graphNodeArray[tj].visited = 1;
	}
}

int main(int argc, char* argv[])
{
	const int numofVertex = 7;//顶点数
	int cost[numofVertex][numofVertex] = {//邻接矩阵存储边的权值
	{ INT_MAX, 12, 5, 11, INT_MAX, INT_MAX, INT_MAX },
	{ 12, INT_MAX, INT_MAX, INT_MAX, 33, INT_MAX, INT_MAX },
	{ 5, INT_MAX, INT_MAX, 21, INT_MAX, 19, INT_MAX },
	{ 11, INT_MAX, 21, INT_MAX, 28, 8, INT_MAX },
	{ INT_MAX, 33, INT_MAX, 28, INT_MAX, INT_MAX, 6},
	{ INT_MAX, INT_MAX, 19, 8, INT_MAX, INT_MAX, 16},
	{ INT_MAX, INT_MAX, INT_MAX, INT_MAX, 6, 16, INT_MAX }
	};
	string verName[numofVertex] = { "A","B","C","D","E","F","G" }; //初始化各顶点
	Graph<string> g(*cost, verName, numofVertex);//调用 Graph 构造函数
	int source;
	cout << "请输入 Prim 算法初始顶点:" << "\n";
	cin >> source;
	try
	{
		g.Prim(source);//调用 Prim 算法
	}
	catch (char*)
	{
		cout << "Prim 算法计算失败！" << endl;
	}
	printf("\n");
	system("pause");
	return 0;
}
