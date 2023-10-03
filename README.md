# Word-Search-And-Count
#include<iostream>
#include<algorithm>
#include<string.h>
#include<map>
#include<fstream>
using namespace std;

// global map to store the word count
map<string, bool> isPrinted;
map<string, int> mp;

// custom a comparator function
bool comp(char s1, char s2)
{
    return tolower(s1) < tolower(s2);
}

// Construct BinarySearchTree class
class BST {
    string word;
    BST *left, *right, *root;
    public:
    BST()
    {
        word = "";
        left = NULL;
        right = NULL;
    }

    BST(string w)
    {
        word = w;
        left = NULL;
        right = NULL;
    }

    // function to insert a word into the BST
    BST* insert(BST *root, string w)
    {
        if(root == NULL)
        {
            transform(w.begin(), w.end(), w.begin(), ::tolower);
            mp[w]++;
            return new BST(w);
        }

        if(lexicographical_compare(root->word.begin(), root->word.end(), w.begin(), w.end(), comp))
        {
            root->right = insert(root->right, w);
        }
        else
        {
            root->left = insert(root->left, w);
        }

        return root;
        }
        // function to search a word from a binary tree
    BST* search(BST *root, string disiredKey){
        string desiredKey;
        BST* currentNode = root;

        while(currentNode){
            if (currentNode->word == desiredKey){
                return currentNode;
            }
            else if (desiredKey < currentNode->word){
                currentNode = currentNode->left;
            }
            else {
                currentNode = currentNode->right;
            }
        }

        return nullptr;
}

    void inOrder(BST *root)
    {
        if(root == NULL)
            return;

        inOrder(root->left);

        if(root->word != "" && !isPrinted[root->word])
        {
            cout<<root->word<<' '<<mp[root->word]<<endl;
            isPrinted[root->word] = true;
        }
        inOrder(root->right);
    }
};

int main()
{
    BST b, *root = NULL, *look= NULL;
    root = b.insert(root, "");
    look = b.search(root, "");
    //read the input file.
    fstream file;
    string fileName = "USconstitutionWords.txt";
    file.open(fileName.c_str());
    string word;
    cout<<"Enter the word you are looking for:";
    string desiredKey;
    cin>>desiredKey;
    while(file >> word)
        b.insert(root, word);
        b.inOrder(root);
        b.search(root, desiredKey);
    if(look != nullptr){
    cout<<"Found your word.";}
    else{
        cout<<"Cannot found your word.";
    }

    return 0;
}
