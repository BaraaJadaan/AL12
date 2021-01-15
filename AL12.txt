#include <iostream>
#include <vector>
#include <string.h>

using namespace std;
string curr_sol;
vector<string> curr;
int n;
string optimal;


bool compare(string part,string current)
{
    for(int i=0;i<part.length();i++)
        for(int j=0;j<current.length();j++)
    if(part[i]==current[j])
        return false;
    return true;
}
void backtrack(int wanted,string curr_sol,int i)
{
    if(i>=n)
    {
        return;
    }
    if(wanted==0)                     //stop condition
    {
        if(curr_sol.size()>optimal.size()) 
        {
            optimal=curr_sol;
        }
        return;
    }
    if(compare(curr[i],curr_sol))
        backtrack(wanted-curr[i].size(),curr_sol+'\n'+curr[i],i+1);
    backtrack(wanted,curr_sol,i+1);
}
int main()
{
    string wanted_word;
    string temp;
    int k = 0;
    cin>>n;
    for(int i=0;i<n;i++)
    {
        cin>>temp;
        curr.push_back(temp);
    }
    cin>>wanted_word;
    backtrack(wanted_word.length(),"",k);
    if(optimal.size()==0)
    {
        cout<<"IMPOSSIBLE";
    }
    else
    {
        cout<<optimal;
    }
}
