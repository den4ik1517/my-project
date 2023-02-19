#include <iostream>

class Resistor{
private:
    std::string type;
    int resistance;
    int power;
    int accuracy;
public:
    std::string get_type(){return type;};
    int get_resistance(){return resistance;};
    int get_power(){return power;};
    int get_accuracy(){return accuracy;};
    Resistor(std::string type1, int resistance1, int power1, int accuracy1){
        type=type1;
        resistance=resistance1;
        power=power1;
        accuracy=accuracy1;
    }
    Resistor(){
        type="d";
        resistance=52;
        power=100;
        accuracy=53;
    }
        friend std::ostream &operator<< (std::ostream &output, const Resistor &other){
            output << other.type << std::endl;
            output << other.resistance << std::endl;
            output << other.power << std::endl;
            output << other.accuracy << std::endl;
            return output;
        };
    bool operator>=(Resistor& other){
        return this->get_accuracy()>=other.get_accuracy();
    }
    bool operator<=(Resistor& other){
        return this->get_accuracy()<=other.get_accuracy();
    }
    bool operator==(Resistor& other){
        return ((this->get_type()==other.get_type())&&(this->get_resistance()==other.get_resistance())&&(this->get_power()==other.get_power())&&(this->get_accuracy()==other.get_accuracy()));
    }

};
class Linked_list {
public:
    Resistor data;
    Linked_list* next;
    Linked_list* previous;
    Linked_list(Resistor resistor){
        data=resistor;
    }
};
void insert(Linked_list* previous, Resistor new_data) {
    Resistor resistor1("a",50,70,56);
    Linked_list* new_list = new Linked_list(resistor1);
    new_list->data = new_data;
    new_list->next = previous->next;
    previous->next=new_list;
}
void insert_by_resistance(Linked_list* pre, Resistor new_data) {
    Resistor resistor1("a",50,70,56);
    Linked_list* new_list = new Linked_list(resistor1);
    new_list->data = new_data;
    class Linked_list* k;
    k=pre->next;
    do{
        if ((k->data.get_resistance()>=k->previous->data.get_resistance())&&(k->data.get_resistance()<=k->next->data.get_resistance())) {
            new_list->next = k->previous->next;
            k->previous->next=new_list;
            break;
        }
        else{
        k= k->next;
        }
    }
    while (k!=pre->next);
}
bool search(Linked_list* current, Resistor resistor){
    class Linked_list* k;
    k=current->next;
    do{
        if (k->data==resistor) {
            return true;
        }
        else{
            return false;
        }
        k= k->next;
    }
    while (k!=current->next);
}
void print_list(Linked_list* last){
    class Linked_list* k;
    k=last->next;
    do{
        std::cout<< k->data << std::endl;
        k= k->next;
        }
    while (k!=last->next);
}
void print_one(Linked_list* one){
    std::cout<<one->data<<std::endl;
}
void delete_one(Linked_list* previous){
    previous->next=previous->next->next;
}
void delete_list(Linked_list** first_ref){
    Linked_list* current = *first_ref;
    Linked_list*next = NULL;
    while (current!=NULL){
        next=current->next;
        free(current);
        current=next;
    }
    *first_ref = NULL;
}
void accuracy_check(Linked_list* last, int accuracyyy){
    class Linked_list* k;
    k=last->next;
        do{
            if (k->data.get_accuracy()>=accuracyyy) {
                std::cout << "this resistor has good accuracy" << std::endl;
                std::cout << k->data << std::endl;
            }
            k= k->next;
        }
        while (k!=last->next);

}
int main(){
    Resistor resistor1("a",50,70,56);
    Resistor resistor2("b",55,90,43);
    Resistor resistor3("c",60,100,49);
    Resistor resistor4;
Linked_list* first = NULL;
Linked_list* second = NULL;
Linked_list* third = NULL;
first= new Linked_list(resistor1);
second = new Linked_list(resistor2);
third = new Linked_list(resistor3);
first->data = resistor1;
first->next= second;
first->previous= third;
second->data= resistor2;
second-> next = third;
second->previous = first;
third-> data=resistor3;
third->next= first;
third->previous= second;
    accuracy_check(third,48);
}