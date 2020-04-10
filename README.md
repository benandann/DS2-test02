//********************************************************************************/ 
// DS2ex02_18_10727217陳炯瑋_10727223陳宇呈 
//********************************************************************************/ 

#include <stdio.h>
#include <iostream>
#include <string.h>
#include <cstdio>
#include <stdlib.h>
#include <vector>
#include <time.h>
#include <fstream>
#include <algorithm>

using namespace std ;

struct inform {
	string schOid ;
	string schName ;
	string depOid ;
	string depName ;
	string day ;
	string dayName ;
	string level ;
	string levelName ;
	string studentNum ;
	string teacherNum ;
	int graduator ;
	string countryNum ;
	string country ;
	string typeNum ;
	string type ;
	int list ;
	bool time = false;
};

struct sortinform {
	int list ;
	int graduator ;
};

struct tNode {
	int data ;
	tNode * leftPtr ;
	tNode * rightPtr ;
	int height ;
	int list ;
};

struct point{
	vector<inform> left;
	vector<inform> right;
	point* theleft;
	point* themid;
	point* theright;
	point* parent;
};

class Job1 {
	public:
		int name = 0;
		vector<inform> store ;
		//vector<sortinform> sorted ;
		
		void Init() {
			store.clear() ;
			//sorted.clear() ;
		} // Init
		
		int DataSize() {
			return store.size() ;
		} // DataSize
		
		void Readfile( string file_name ) {
				int i = 1 ;
				char c ;
				char a;
				int size = 1000 ;
				char * line  = new char[size] ; // 讀垃圾
				char * testinform = new char[size] ;
				inform tempinform ;
				point *head = NULL;
				FILE * file ;
				string tempfile_name = file_name ;
			    tempfile_name = "input" + file_name + ".txt" ;
				file = fopen( tempfile_name.c_str(), "r" ) ;
				if ( file == NULL )
				    cout << "### " << tempfile_name << " does not exist! ###" << endl ;
			    else {
			    	fscanf( file, "%[^\n]%*c", line ) ;
			    	fscanf( file, "%[^\n]%*c", line ) ;
			    	fscanf( file, "%[^\n]%*c", line ) ;

					while ( fscanf( file, "%s", testinform ) != EOF ) {
						tempinform.schOid = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.schName = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.depOid = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.depName = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.day = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.dayName = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.level = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.levelName = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.studentNum = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.teacherNum = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.graduator = atoi(testinform) ;
						fscanf( file, "%s", testinform ) ;
						tempinform.countryNum = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.country = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.typeNum = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.type = testinform ;
						while(c != '\n' && fscanf(file, "%c", &c) != -1){

						}
						tempinform.list = i ;
						tree(head, head, tempinform) ;
						i++ ;
					
						store.push_back( tempinform ) ;
					} // while
					
					int height = 1;
					testheight( head, height);
					cout <<"tree height = "<<height<<endl;
					
					int nodenum = 1;
					name = 0;
					head->left[0].time = true;
					head->right[0].time = true;
					int i = nodenumber( head, nodenum);
					cout << "Number of nodes = " << i<<endl;
					
					output1(head);
					/*if ( head->left[0].list <  head->right[0].list  ){   //左比右小 
					
						for ( int i = 0; i < head->left.size(); i++){
							cout << head->left[i].schName << head->left[i].list << "@@" << endl;								
						}
						for ( int i = 0; i < head->right.size(); i++){
							cout << head->right[i].schName << head->right[i].list << "@@" << endl;	
						}
					}
					else if ( head->left[0].list >  head->right[0].list  ){  //左比右大 
						for ( int i = 0; i < head->right.size(); i++){
							cout << head->right[i].schName << head->right[i].list << "@@" << endl;	
						}
						for ( int i = 0; i < head->left.size(); i++){
							cout << head->left[i].schName << head->left[i].list << "@@" << endl;								
						}
					}
					else{    //只有一項 
						for ( int i = 0; i < head->right.size(); i++){
							cout << head->right[i].schName << head->right[i].list << "@@" << endl;	
						}
					}	*/								
					
					
					delete [] line ;
					delete [] testinform ;
					fclose( file ) ;
				} // else
			
		} // Readfile
		
			
		void test () {
			int site = 0, size = store.size() ;
			for ( ; site < size ; site++ ) {
				cout << store.at(site).schName << "\t" << store.at(site).graduator << endl ;
			} // for
		}   // test*/	
		
		void testheight(point* head, int &height){
			
			point * temp = head;
			if (temp->theleft != NULL){
				height++;
				testheight(temp->theleft,height);
			}
		}
		
		
		/*void nodenumber(point* head, int &nodenum){
			
			if( head->theleft != NULL && head->theleft->left[0].time == false ){
				head->theleft->left[0].time = true;
				nodenum++;
				nodenumber(head->theleft,nodenum);
				return;
			}
			else if( head->theright != NULL && head->theright->left[0].time == false ){
				head->theright->left[0].time = true;
				nodenum++;
				nodenumber(head->theright,nodenum);
				return;
			}
			else if( head->themid != NULL && head->themid->left[0].time == false ){
				head->themid->left[0].time = true;
				nodenum++;
				nodenumber(head->themid,nodenum);
				return;
			}
			return;
		}*/
		
		int nodenumber(point* head, int nodenum){
			if(head == NULL)
				return name;
			name++;
			nodenumber(head->theleft,nodenum);
			
			nodenumber(head->themid,nodenum);
			
			nodenumber(head->theright,nodenum);	
								
		}
		
		void output1(point* head){
			int i = 0,j=1;
			point* temp = head;
			if ( head->left[0].list <  head->right[0].list  ){   //左比右小
				for ( int i = 0; i < head->left.size(); i++){ 
					cout << j<< ": " << "[" << head->left[i].list << "]" << head->left[i].schName << ", " << head->left[i].depName << ", " << head->left[i].day << " "
				 	 << head->left[i].dayName << ", "<< head->left[i].level << " "<<  head->left[i].levelName << ", " <<  head->left[i].graduator <<endl; 
					j++;
				}
				for( i = 0; i < head->right.size() ; i++ ) {   
					cout << j<< ": " << "[" << head->right[i].list << "]" << head->right[i].schName << ", " << head->right[i].depName << ", " << head->right[i].day << " "
				 	 	<< head->right[i].dayName << ", "<< head->right[i].level << " "<<  head->right[i].levelName << ", " <<  head->right[i].graduator<<endl; 
					j++;
				}
			}
			else if (head->left[0].list >  head->right[0].list ){   //左比右大 
			
				for( i = 0; i < head->right.size() ; i++ ) {
					cout << j<< ": " << "[" << head->right[i].list << "]" << head->right[i].schName << ", " << head->right[i].depName << ", " << head->right[i].day << " "
				 	 	<< head->right[i].dayName << ", "<< head->right[i].level << " "<<  head->right[i].levelName << ", " <<  head->right[i].graduator<<endl; 
					j++;
				}
				for ( int i = 0; i < head->left.size(); i++){ 
					cout << j<< ": " << "[" << head->left[i].list << "]" << head->left[i].schName << ", " << head->left[i].depName << ", " << head->left[i].day << " "
				 	 << head->left[i].dayName << ", "<< head->left[i].level << " "<<  head->left[i].levelName << ", " <<  head->left[i].graduator <<endl; 
					j++;
				}
			}
			else{   //只有一項 
				for ( int i = 0; i < head->left.size(); i++){ 
					cout << j<< ": " << "[" << head->left[i].list << "]" << head->left[i].schName << ", " << head->left[i].depName << ", " << head->left[i].day << " "
				 	 << head->left[i].dayName << ", "<< head->left[i].level << " "<<  head->left[i].levelName << ", " <<  head->left[i].graduator <<endl; 
					j++;
				}
				
			}
		}
		
		void tree(point* &head, point *temp, inform data) {      // 建23樹 
			point *temp2 = NULL;
			createnode( temp2, data);    //放新資料 		
			vector<inform> test ;
			if ( head == NULL){
				createnode ( head, data);	
				
				return;
			}	
			if ( strcmp(temp -> left[0].schName.c_str(), data.schName.c_str()) == 0 ){
				temp->left.push_back(data) ;
				return;
			}
			else if ( strcmp(temp -> right[0].schName.c_str(), data.schName.c_str()) == 0  ){
				temp->right.push_back(data) ;
				return;
			}
			if(strcmp(temp->left[0].schName.c_str(), data.schName.c_str() ) > 0 ){     //新資料比左邊小 
				if (temp->theleft != NULL )  {  // 不是樹葉
					tree( head,temp->theleft, data);
				}
				else if ( temp->theleft == NULL && strcmp(temp -> left[0].schName.c_str(), temp -> right[0].schName.c_str()) == 0)  {  // 樹葉&&只有一項
					temp -> right = temp -> left ; 
					temp -> left = test ;
					temp -> left.push_back(data) ;
					//cout << temp -> left[0].schName << "\t" << temp -> right[0].schName << endl ;
					return;
				}
				else if ( temp->theleft == NULL && strcmp(temp -> left[0].schName.c_str(), temp -> right[0].schName.c_str()) != 0) {  // 樹葉&& 有兩項 
					spilt(head,temp,temp2);
					
				}
				
			}
			if(strcmp(temp -> right[0].schName.c_str(), data.schName.c_str()) < 0){      //新資料比右邊大 
				if (temp -> theright == NULL && strcmp(temp -> left[0].schName.c_str(), temp -> right[0].schName.c_str()) == 0)  {  // 樹葉&&只有一項
					
					temp->right[0] = data;
					
					return;
				}
				else if ( temp->theright == NULL && strcmp(temp -> left[0].schName.c_str(), temp -> right[0].schName.c_str()) != 0) {// 樹葉&& 有兩項 
					spilt (head,temp,temp2);
				}
				else if (temp->theright != NULL ) {// 不是樹葉
					tree( head,temp->theright, data); 
				}
			}
			if(temp->themid != NULL && strcmp(temp->left[0].schName.c_str(),data.schName.c_str())< 0 &&strcmp(temp->right[0].schName.c_str(), data.schName.c_str()) > 0){ //不是樹葉&&在兩樹之間 
				tree( head,temp->themid, data);		 
			} 
			else if(temp->themid == NULL && strcmp(temp->left[0].schName.c_str(),data.schName.c_str())< 0 &&strcmp(temp->right[0].schName.c_str(), data.schName.c_str()) > 0){ // 是樹葉&&在兩樹之間
				spilt (head,temp,temp2);
				
			}
		}
		
				
		void spilt (point* &head,point* temp,point* temp2 ){
			point* temp3 = NULL ;  // 暫時的head 
			point* temp4 = NULL ;
			vector<inform> data;
			
			if ( temp ->parent == NULL  ) {   // head要分裂    temp = head			
				if ( strcmp(temp -> left[0].schName.c_str(), temp2 -> left[0].schName.c_str() ) > 0 ) {  // 比head的左邊小 V
					createparentnode( temp3, temp -> left ) ;
					temp->left = temp->right;
					temp3->theright = temp;
					temp3->theleft = temp2;					
					temp->parent =temp3;
					temp2->parent =temp3;
					head = temp3; 										
				}
				else if ( strcmp(temp -> right[0].schName.c_str(), temp2 -> left[0].schName.c_str()) < 0 ) {  // 比head的右邊大  
					createparentnode( temp3, temp -> right ) ;
					temp->right = temp->left;
					temp3->theright = temp2;
					temp3->theleft = temp;					
					temp->parent =temp3;
					temp2->parent =temp3;
					head = temp3;					
				}
				else if (strcmp(temp -> right[0].schName.c_str(), temp2 -> left[0].schName.c_str()) > 0 && strcmp(temp -> left[0].schName.c_str(), temp2 -> left[0].schName.c_str()) < 0) { //在head兩數中間
					createparentnode( temp3, temp -> left ) ;
					temp->left = temp->right;     //temp3左   temp右 
					if ( temp -> theleft != NULL && temp -> theright != NULL ) {  //不是樹葉 ?????????????????
					 	temp3->theleft = temp->theleft;
					 	temp->theleft->parent = temp3;
					 	temp->theleft = temp2->theright;//VVVVVVVVV
					 	temp2->theright->parent = temp;
					 	
					 	temp3->theright = temp2->theleft;
					 	temp2->theleft->parent = temp3;
					 	
					 	
					}
					temp2 -> theleft = temp3 ;
					temp3 -> parent = temp2 ;
					temp2 -> theright = temp ;
					temp -> parent = temp2 ;
					head = temp2 ;
					
				}
				
				return;	
			}
			else if( temp -> parent -> left[0].list == temp -> parent -> right[0].list){   //樹葉的分裂 ((父節點只有一個)) 
				spilt2(head, temp, temp2);
			}
			else if( temp -> parent -> left[0].list != temp -> parent -> right[0].list){   //樹葉的分裂 ((父節點有兩個))
				spilt3(head, temp, temp2);
			}
			
		}
		
		void spilt2( point* &head,point* temp,point* temp2 ){
			point* temp3 =NULL;
			
			if ( strcmp( temp -> left[0].schName.c_str(), temp2 -> left[0].schName.c_str()) > 0 ){  //資料小於左 
				createparentnode( temp3, temp -> left ) ;
				temp->left = temp->right;
					
			if ( temp->parent->theleft == temp ){ // 在父節點的左   
					temp = temp->parent;
						//temp->right = temp->left;//*
					temp->left = temp3->left;
					temp->themid = temp->theleft;
					temp->theleft = temp2;
					temp2->parent = temp;						
				}
				else if (temp->parent->theright == temp ) {  // 在父節點的右 
					temp = temp->parent;
					temp->themid = temp2;//*
					temp->right = temp3->right;
						
					temp2->parent = temp;
				}
			}
			else if ( strcmp( temp -> right[0].schName.c_str(), temp2 -> left[0].schName.c_str()) < 0 ){  //資料大於右 
					
				createparentnode( temp3, temp -> right ) ;
				temp->right = temp->left;
				if ( temp->parent->theleft == temp ){ // 在父節點的左   V
					temp = temp->parent;
					temp->themid = temp2;
					temp->left = temp3->left;
						
					temp2->parent = temp;												
				}
				else if ( temp->parent->theright == temp ){ // 在父節點的右
					temp = temp->parent;
					temp->right = temp3->left;
					temp->themid = temp->theright;
					temp->theright = temp2;
					temp2->parent = temp;
				} 
			} 
			else if(strcmp(temp->right[0].schName.c_str(), temp2->left[0].schName.c_str()) > 0 &&strcmp(temp->left[0].schName.c_str(),temp2->left[0].schName.c_str()) < 0){  // 資料在兩數中間
					
				createparentnode(temp3, temp -> left) ;
				temp -> left = temp -> right ;   	
				if ( temp -> theleft != NULL && temp -> theright != NULL ) {  //不是樹葉        ????????????  
				 	temp3 -> theleft = temp -> theleft ;
					temp -> theleft -> parent = temp3 ;
						
					temp3 -> theright = temp2 -> theleft ;//*
					temp2 -> theleft -> parent = temp3 ;
						
					temp -> theleft = temp2 -> theright ;
					temp2 -> theright -> parent = temp ;
				}
					
				temp2 -> theleft = temp3 ;  //temp2佐是temp3 V
				temp3 -> parent = temp2 ;
				temp2 -> theright = temp ;  	//temp2右是temp
			   		
				if (temp->parent->theleft == temp ){ // 在父節點的左 cj0
					temp = temp -> parent ;
					temp -> right = temp -> left ;
					temp -> left = temp2 -> left ;
						
					temp -> theleft = temp2 -> theleft ;
					temp2 -> theleft -> parent = temp ;
						
					temp -> themid = temp2 -> theright ;
					temp2 -> theright -> parent = temp ;
						
				}
				else if (temp->parent->theright == temp ) { // 在父節點的右   ck0
					temp = temp->parent;
					temp -> right = temp2 -> left ;
						
					temp -> themid = temp2 -> theleft ;
					temp2 -> theleft -> parent = temp ;

                    temp -> theright = temp2 -> theright ;//*
					temp2 -> theright -> parent = temp ;
				}
			}
				
			return;			
		} 	
	
		
		void spilt3( point* &head,point* temp,point* temp2 ){
			point* temp3 = NULL;
			point* temp4 = NULL;
			if( temp -> parent -> left[0].list != temp -> parent -> right[0].list){   //樹葉的分裂 ((父節點有兩個)) 
					
				if ( strcmp( temp -> left[0].schName.c_str(), temp2 -> left[0].schName.c_str()) > 0 ){  //資料小於左 
					createparentnode( temp3, temp -> left ) ;
					temp->left = temp->right;
					if ( temp->parent->theleft == temp ){ // 在父節點的左 V
						temp3 -> theleft = temp2 ;
						temp2 -> parent = temp3 ;
						temp3 -> theright = temp ;
					
						temp4 = temp -> parent ;//紀錄父節點 
						temp -> parent = temp3 ;
						temp4 -> theleft = temp4 -> themid ;
						temp4 -> themid = NULL ;
					}
					else if (temp->parent->theright == temp ) {   // 在父節點的右 V
						temp3 -> theleft = temp2 ;
						temp2 -> parent = temp3 ;
						temp3 -> theright = temp ;
						temp4 = temp -> parent ;//紀錄父節點 
						temp -> parent = temp3 ;
						temp4 -> theright = temp4 -> themid ;
						temp4 -> themid = NULL ;
					}
					else if (temp->parent->themid == temp ) {   // 在父節點的中		V							
						temp3 -> theleft = temp2 ;
						temp2 -> parent = temp3 ;
						temp3 -> theright = temp ;
						temp4 = temp -> parent ;//紀錄父節點 
						temp -> parent = temp3 ;
						temp4 -> themid = NULL ;
					}
					spilt(head, temp4, temp3) ;
				}
				else if ( strcmp( temp -> right[0].schName.c_str(), temp2 -> left[0].schName.c_str()) < 0 ){  //資料大於右 
					createparentnode( temp3, temp -> right ) ;
					temp->right = temp->left;
					if ( temp->parent->theleft == temp ){ // 在父節點的左 cj0
						temp3 -> theright = temp2 ; 
						temp3 -> theleft = temp ;//*
						temp2 -> parent = temp3 ;
						
						temp4 = temp -> parent ;
						temp -> parent = temp3 ;
						temp4 -> theleft = temp4 -> themid ;
						temp4 -> themid = NULL ;
					}
					else if ( temp->parent->theright == temp ){ // 在父節點的右  cu0
						temp3 -> theright = temp2 ;
						temp3 -> theleft = temp ;//*
						temp2 -> parent = temp3 ;
						
						temp4 = temp -> parent ;
						temp -> parent = temp3 ;
						temp4 -> theright = temp4 -> themid ;
						temp4 -> themid = NULL ;
					} 
					else if ( temp->parent->themid == temp ){ // 在父節點的中 
						temp3 -> theright = temp2 ;
						temp3 -> theleft = temp ;//*
						temp2 -> parent = temp3 ;
						
						temp4 = temp -> parent ;
						temp -> parent = temp3 ;
						temp4 -> themid = NULL ;
						
					} 
					spilt(head, temp4, temp3) ;
				} 
				else if(strcmp(temp->right[0].schName.c_str(), temp2->left[0].schName.c_str()) > 0 &&strcmp(temp->left[0].schName.c_str(),temp2->left[0].schName.c_str()) < 0){  // 資料在兩數中間
					createparentnode(temp3, temp -> left) ;
					temp -> left = temp -> right ;   	
					if ( temp -> theleft != NULL  ) {  //不是樹葉        ????????????
							 temp3->theleft = temp->theleft;
					 		temp->theleft->parent = temp3;
					 		
					 		temp3->theright = temp2->theleft;
					 		temp2->theleft->parent = temp3;
					 							 		
					 		temp->theleft = temp2->theright;
					 		temp2->theright->parent = temp;
					}
					if (temp->parent->theleft == temp ){ // 在父節點的左 
						
						temp2->theleft = temp3; // V
						temp3->parent = temp2;
						temp2->theright = temp;
						temp4= temp->parent;//紀錄父節點
						temp->parent = temp2;
						temp4->theleft = temp4->themid;
						temp4->themid = NULL;			
			
					}
					else if (temp->parent->theright == temp ){ // 在父節點的右 
						
						temp2->theleft = temp3; // V
						temp3->parent = temp2;
						temp2->theright = temp;
						temp4= temp->parent;//紀錄父節點
						temp->parent = temp2;
						temp4->theright = temp4->themid;
						temp4->themid = NULL;
			
					}
					else if (temp->parent->themid == temp ){ // 在父節點的中
						
						temp2->theleft = temp3;//V
						temp3->parent = temp2;
						temp2->theright = temp;
						temp4= temp->parent;//紀錄父節點
						temp->parent = temp2;
						temp4->themid = NULL;
					} 
					spilt(head, temp4, temp2) ;
				}						
			}
		}
		void createnode (point *&temp, inform data) {
			temp = new point;			
			temp -> left.push_back(data) ;
			temp -> right.push_back(data) ;
			temp -> theleft = NULL ;
			temp -> themid = NULL ;
			temp -> theright = NULL ;
			temp -> parent = NULL ;
		}
		
		void createparentnode (point *&temp, vector<inform> data){
			temp = new point;		
			temp -> left = data ;
			temp -> right= data ;
			temp -> theleft = NULL ;
			temp -> themid = NULL ;
			temp -> theright = NULL ;
			temp -> parent = NULL ;
		}
	
};

class Job2 {
	public :
		vector<inform> store ;
		vector<sortinform> sorted ;
		vector<int> count ;
		
		void Init() {
			store.clear() ;
			sorted.clear() ;
			count.clear() ;
		} // Init
		
		int DataSize() {
			return store.size() ;
		} // DataSize
		
		void Readfile( string file_name ) {
				int i = 1 ;
				int size = 1000 ;
				char * line  = new char[size] ; // 讀垃圾
				char * testinform = new char[size] ;
				inform tempinform ;
				FILE * file ;
				string tempfile_name = file_name ;
			    tempfile_name = "input" + file_name + ".txt" ;
				file = fopen( tempfile_name.c_str(), "r" ) ;
				if ( file == NULL )
				    cout << "### " << tempfile_name << " does not exist! ###" << endl ;
			    else {
			    	fscanf( file, "%[^\n]%*c", line ) ;
			    	fscanf( file, "%[^\n]%*c", line ) ;
			    	fscanf( file, "%[^\n]%*c", line ) ;
	    	
					while ( fscanf( file, "%s", testinform ) != EOF ) {
						tempinform.schOid = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.schName = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.depOid = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.depName = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.day = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.dayName = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.level = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.levelName = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.studentNum = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.teacherNum = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.graduator = atoi(testinform) ;
						fscanf( file, "%s", testinform ) ;
						tempinform.countryNum = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.country = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.typeNum = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.type = testinform ;
						
						tempinform.list = i ;
						i++ ;
					
						store.push_back( tempinform ) ;
					} // while
				
					delete [] line ;
					delete [] testinform ;
					fclose( file ) ;
				} // else
			
			} // Readfile
			
			// **********************************任務二***********************************************
				
			int height( tNode * N ) {
				if ( N == NULL )
					return 0 ;
				return N->height ;
			} // height
				
			int treeHeight( tNode * root ) {
				if ( root == NULL )
					return 0 ;
				return max( treeHeight( root->leftPtr), treeHeight( root->rightPtr) ) + 1 ;
			} // treeHeight
			
			void FindGraduator( tNode * N ) {
				int j = 1 ;
				for ( int i = 0 ; i < store.size() ; i++ ) {
					if (  N->data == store.at(i).graduator ) {
						cout << j << ": [" << store.at(i).list << "] " << " " ;
						cout << store.at(i).schName << ", " << store.at(i).depName  << ", " ;
						cout << store.at(i).day << " " << store.at(i).dayName << ", " ;
						cout << store.at(i).level << " " << store.at(i).levelName << ", " ;
						cout << store.at(i).graduator << endl ;
						j++ ;	
					} // if
				} // for
			} // FindGraduator
			
			void preOrder( tNode * root ) {
				int temp = 0 ;
				if ( root != NULL ) {
					preOrder( root->leftPtr ) ;
					temp = root->data ;
					count.push_back( temp ) ;
					preOrder( root->rightPtr ) ;
				} // if
			} // preOrder
			
			tNode * newNode( int data, int list ) {
				tNode * newNode = new tNode() ;
				newNode->data = data ;
				newNode->leftPtr = NULL ;
				newNode->rightPtr = NULL ;
				newNode->height = 1 ;
				newNode->list = list ;
			
				return( newNode ) ;
			} // newNode
			
			tNode * rightRotate( tNode * y ) {
				tNode * x = y->leftPtr ;
				tNode * temp = x->rightPtr ;
			
				x->rightPtr = y ;
				y->leftPtr = temp ;
			
				y->height = max( height( y->leftPtr ), height( y->rightPtr ) ) + 1 ;
				x->height = max( height( x->leftPtr ), height( x->rightPtr ) ) + 1 ;
			
				return x ;
			
			} // rightRotate
		
			tNode * leftRotate( tNode * x ) {
				tNode * y = x->rightPtr ;
				tNode * temp = y->leftPtr ;
				
				y->leftPtr = x ;
				x->rightPtr = temp ;
			
				x->height = max( height( x->leftPtr ), height( x->rightPtr ) ) + 1 ;
				y->height = max( height( y->leftPtr ), height( y->rightPtr ) ) + 1 ;
			
				return y ;
			} // leftRotate
		
			int Balance( tNode * N ) {
				if ( N == NULL )
					return 0 ;
				return ( height( N->leftPtr ) - height( N->rightPtr ) ) ;
			} // Balance
		
			tNode * Insert( tNode * N, int data, int list ) {
				if ( N == NULL )
					return( newNode( data, list ) ) ;
				
				if ( data < N->data )
					N->leftPtr = Insert( N->leftPtr, data, list ) ;
				else if ( data > N->data )
					N->rightPtr = Insert( N->rightPtr, data, list ) ;
				else
					return N ;
				
				N->height = 1 + max( height( N->leftPtr), height( N->rightPtr ) ) ;
			
				int balance = Balance( N ) ;
			
				if ( balance > 1 && data < N->leftPtr->data )
					return rightRotate( N ) ;
			
				if ( balance < -1 && data > N->rightPtr->data )
					return leftRotate( N ) ;
			
				if ( balance > 1 && data > N->leftPtr->data ) {
					N->leftPtr = leftRotate( N->leftPtr ) ;
					return rightRotate( N ) ;
				} // if
			
				if ( balance < -1 && data < N->rightPtr->data ) {
					N->rightPtr = rightRotate( N->rightPtr ) ;
					return leftRotate( N ) ;
				} // if
			
				return N ;
			
			} // Insert
			
};

int main(int argc, char** argv) {
	int num = 0 ;
	int temp = 0 ;
	int templist = 0 ;
	tNode* root = NULL ;
	bool done = false ;
	string file_name ;
	Job1 tree23 ;
	Job2 avltree ;
	do {
		cout << "*** Search Tree Utilities **" << endl ;
		cout << "* 0. QUIT                  *" << endl ;
		cout << "* 1. Build 2-3 tree        *" << endl ;
		cout << "* 2. Build  AVL tree       *" << endl ;
		cout << "****************************" << endl ;
		cout << "Input a choice(0, 1, 2): " ;
		
		cin >> num ;
		if ( num == 0 )
		    done = true ;
		else if ( num == 1 ) {
			cout << "Input a file number ([0] Quit): " ;
			cin >> file_name ;
			if ( file_name != "0" ) {
				tree23.Readfile( file_name ) ;
			} // if 
		} // else if
		else if ( num == 2 ) {
			cout << "Input a file number ([0] Quit): " ;
			cin >> file_name ;
			avltree.Readfile( file_name ) ;
			if ( file_name != "0" ) {
				for ( int i = 0 ; i < avltree.DataSize() ; i++ ) {
					temp = avltree.store.at(i).graduator ; 
					templist = avltree.store.at(i).list ;
					root = avltree.Insert( root, temp, templist ) ;
				} // for
				
				avltree.preOrder( root ) ;
				
				cout << "Tree height = " << avltree.treeHeight( root ) << endl ;
				cout << "Number of nodes = " << avltree.count.size() << endl ;
				avltree.FindGraduator( root ) ;
				avltree.Init() ;
				root = NULL ;
			} // if
		} // esle if
		
	
		
	} while( !done ) ;
		
} // main
