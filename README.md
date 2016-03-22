The 坑 of C++
===============

列举在C++中遇到的坑

---------------

### operator=

**operator=**的实现者必须考虑自赋值（如：**x=x**）的情况。



### 反人类的反向迭代器删除

    MapX::reverse_iterator it = oMap.rbegin();
    oMap.erase((++it).base());

使用者必须理解reverse_iterator和iterator之间的对应关系(base函数),然后才知道应该++再删除

好的接口设计应该直接提供支持反向迭代器删除的erase函数,就像如下:

    void erase (reverse_iterator position);

附base函数的说明:

    The base iterator is an iterator of the same type as the one used to construct the reverse_iterator, but pointing to the element next to the one the reverse_iterator is currently pointing to (a reverse_iterator has always an offset of -1 with respect to its base iterator).
