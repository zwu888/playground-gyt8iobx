# Cyclic reference with std::shared_ptr
```C++ runnable
#include <iostream>
#include <type_traits>
#include <memory>
struct Node {  // Binary tree
    Node() { std::cout << "c'tor" << std::endl; }
    ~Node() { std::cout << "d'tor" << std::endl; }
    std::weak_ptr<Node> parent;
    std::shared_ptr<Node> left;
    std::shared_ptr<Node> right;
};
int main() {
      auto root = std::make_shared<Node>();
      root->left = std::make_shared<Node>();
      root->left->parent = root;
}
