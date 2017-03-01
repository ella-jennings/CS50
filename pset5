/**
 * Implements a dictionary's functionality.
 */

#include <stdbool.h>
#include <stdio.h>
#include <stdlib.h>
#include "dictionary.h"
#include "string.h"

// DEFINE GLOBAL VARIABLES
int word_count = 0;
int total_nodes = 0;
#define ALPHABET 27

// DEFINE NODE STRUCTURE
typedef struct node
{
    bool is_word;
    struct node *children[ALPHABET];
}
node;

// CREATE ROOT NODE
node *root;

 

// DEFINE FUNCTIONS
int index(int);
bool checknode(node*);
void unload_node(node*);


/**
 * Returns true if word is in dictionary else false.
 */
 
bool check(const char *word)
{
    
    // declare useful names
    node *current_node = root;
    
    for(int i = 0; i < strlen(word); i++)
    {
        char letter = word[i];
        int n = index(letter);
        
        //if node -> next node = null, return false
        if(current_node -> children[n] == NULL)
        {
            return false;
        }
        
        else
        {
            current_node = current_node -> children[n];
        }
    }
    //printf("reached end of loop\n");
    
    if(current_node -> is_word == 1)
    {
        //printf("found word\n");
        return true;
    }
    
    return false;
}



/**
 * Loads dictionary into memory. Returns true if successful else false.
 */
 
bool load(const char *dictionary)
{
    
    
    // LOAD DICTIONARY
    FILE *dict = fopen(dictionary, "r");
    if(dict == NULL) {
        printf("error opening file");
        return false;
    }
    
    // ALLOCATE SPACE TO ROOT
    root = calloc(1, sizeof(node));
    if(checknode(root) == true)
    {
        total_nodes++;
    }
    
    // CREATE CURSOR AND CHARACTER
    node *current_node = root;
    char word[LENGTH];
    
    
    // FOR EACH CHARACTER IN DICTIONARY
    while(fscanf(dict, "%s", word) != EOF)
    {
        for(int i = 0; i < strlen(word); i++)
        {
            char letter = word[i];
            int n = index(letter);
            
            // IF NODE EXISTS THEN POINT TO NEXT NODE
            if(current_node -> children[n] != NULL)
            {
                current_node = current_node -> children[n];
                //printf("moved to children[%i] for letter %c\n", n, letter);
            }
                
            // IF NODE DOESN'T EXIST, CREATE IT AND SET CURRENT TO NEW NODE
            else if(current_node -> children[n]== NULL)
            {
                current_node -> children[n] = calloc(1, sizeof(node));
                if(checknode(current_node -> children[n]) == true)
                {
                    total_nodes++;
                }
                
                //printf("node created, children[%i] for letter %c\n", n, letter);
                current_node = current_node -> children[n];
                
            }
        }
        
        
        // HIGHLIGHT END OF WORD
        current_node -> is_word = true;
        word_count++;
        current_node = root;
        //printf("end of word, moving to root\n");
    }
    
    //printf("total nodes created = %i\n", total_nodes);
    
    
    // CLOSE DICTIONARY
    fclose(dict);
    
    for(int i = 0; i < ALPHABET; i++)
    {
    }
    
    //printf("%i\n",root -> children[2] -> children[0]->is_word);
    
    return true;
}



/**
 * Returns number of words in dictionary if loaded else 0 if not yet loaded.
 */
unsigned int size(void)
{
    return word_count;
}



/**
 * Unloads dictionary from memory. Returns true if successful else false.
 */
bool unload(void)
{
    unload_node(root);
    printf("Ella's version");
    return true;
}

// extra functions

/**
 * Index function *
 * takes ascii characters and returns children values 0-26
 * returning 30 indicates error
 **/
int index(int letter) 
{
    // uppercase
    if(letter > 64 && letter < 91)
    {
        letter = letter % 65;
    }
    
    // lowercase
    else if(letter > 96 && letter < 123)
    {
        letter = letter % 97;
        
    }
    
    // apostrophe
    else
    {
        letter = 26;
    }
    
    return letter;
}

/**
 * Checks if a node has been allocated properly
 **/
 
bool checknode(node *name)
{
    if(name == NULL)
    {
        printf("Error creating node\n");
        unload();
        return false;
    }
    return true;
}

void unload_node(node* current_node)
{
     for(int n = 0; n < ALPHABET; n++)
    {
            if(current_node -> children[n] != NULL)
            {
                unload_node(current_node -> children[n]);
            }
      
    }
    free(current_node);
    return;
}
