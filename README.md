# lldb_dump_class_layout
LLDB script for dumping C++ structs/classes and variables layout in memory

Works with Xcode/Android Studio, Visual Studio Code
(For Visual Studio Code, use binary from https://github.com/vadimcn/vscode-lldb)

After start lldb, use command:
`command script import ~/PATH_TO_SCRIPT/dump_class_laouyt.py` to install commands `layout` and `layoutvar`

Example of usage:

```
(lldb) layoutvar aaa
std::__1::map<int, int, std::__1::less<int>, SimpleAllocator<std::__1::pair<const int, int> > >
 +0 < 24> std::__1::map<int, int, std::__1::less<int>, SimpleAllocator<std::__1::pair<const int, int> > >
 +0 < 24>   std::__1::map<int, int, std::__1::less<int>, SimpleAllocator<std::__1::pair<const int, int> > >::__base __tree_
 +0 < 8>    std::__1::__tree<std::__1::__value_type<int, int>, std::__1::__map_value_compare<int, std::__1::__value_type<int, int>, std::__1::less<int>, true>, SimpleAllocator<std::__1::__value_type<int, int> > >::__iter_pointer __begin_node_
 +8 < 8>     std::__1::__compressed_pair<std::__1::__tree_end_node<std::__1::__tree_node_base<void *> *>, SimpleAllocator<std::__1::__tree_node<std::__1::__value_type<int, int>, void *> > > __pair1_
 +8 < 8>       std::__1::__compressed_pair_elem<std::__1::__tree_end_node<std::__1::__tree_node_base<void *> *>, 0, false> std::__1::__compressed_pair_elem<std::__1::__tree_end_node<std::__1::__tree_node_base<void *> *>, 0, false>
 +8 < 8>         std::__1::__tree_end_node<std::__1::__tree_node_base<void *> *> __value_
 +8 < 8>          std::__1::__tree_end_node<std::__1::__tree_node_base<void *> *>::pointer __left_
 +8 < 1>       std::__1::__compressed_pair_elem<SimpleAllocator<std::__1::__tree_node<std::__1::__value_type<int, int>, void *> >, 1, true> std::__1::__compressed_pair_elem<SimpleAllocator<std::__1::__tree_node<std::__1::__value_type<int, int>, void *> >, 1, true>
 +8 < 1>         SimpleAllocator<std::__1::__tree_node<std::__1::__value_type<int, int>, void *> > SimpleAllocator<std::__1::__tree_node<std::__1::__value_type<int, int>, void *> >
 +8 < 1>           std::__1::allocator<std::__1::__tree_node<std::__1::__value_type<int, int>, void *> > std::__1::allocator<std::__1::__tree_node<std::__1::__value_type<int, int>, void *> >
 +16 < 8>     std::__1::__compressed_pair<unsigned long, std::__1::__map_value_compare<int, std::__1::__value_type<int, int>, std::__1::less<int>, true> > __pair3_
 +16 < 8>       std::__1::__compressed_pair_elem<unsigned long, 0, false> std::__1::__compressed_pair_elem<unsigned long, 0, false>
 +16 < 8>        unsigned long __value_
 +16 < 1>       std::__1::__compressed_pair_elem<std::__1::__map_value_compare<int, std::__1::__value_type<int, int>, std::__1::less<int>, true>, 1, true> std::__1::__compressed_pair_elem<std::__1::__map_value_compare<int, std::__1::__value_type<int, int>, std::__1::less<int>, true>, 1, true>
 +16 < 1>         std::__1::__map_value_compare<int, std::__1::__value_type<int, int>, std::__1::less<int>, true> std::__1::__map_value_compare<int, std::__1::__value_type<int, int>, std::__1::less<int>, true>
 +16 < 1>           std::__1::less<int> std::__1::less<int>
 +16 < 1>             std::__1::binary_function<int, int, bool> std::__1::binary_function<int, int, bool>
Total byte size: 24
Total pad bytes: 0
(lldb) layout "std::__1::__tree_node<std::__1::__value_type<int, int>, void *>"
 +0 < 40> std::__1::__tree_node<std::__1::__value_type<int, int>, void *>
 +0 < 32>   std::__1::__tree_node_base<void *> std::__1::__tree_node_base<void *>
 +0 < 8>     std::__1::__tree_node_base_types<void *>::__end_node_type std::__1::__tree_node_base_types<void *>::__end_node_type
 +0 < 8>      std::__1::__tree_end_node<std::__1::__tree_node_base<void *> *>::pointer __left_
 +8 < 8>    std::__1::__tree_node_base<void *>::pointer __right_
 +16 < 8>    std::__1::__tree_node_base<void *>::__parent_pointer __parent_
 +24 < 1>    bool __is_black_
 +25 < 3>  <PADDING: 3 bytes>
 +28 < 8>   std::__1::__tree_node<std::__1::__value_type<int, int>, void *>::__node_value_type __value_
 +28 < 8>     std::__1::__value_type<int, int>::value_type __cc
 +28 < 4>      const int first
 +32 < 4>      int second
 +36 < 4>  <PADDING: 4 bytes>
Total byte size: 40
Total pad bytes: 7
Padding percentage: 17.50 %
```

Issues:
Script shows incorrect paddings between virtual ancestors of the object
