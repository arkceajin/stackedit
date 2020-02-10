1. std::move
    after **C++11**, could

    `void set_name(const std::string& name);`

    or

    ```
    void set_name(std::string&& name);
    std::string name = "123123";
    set_name(static_cast<std::string&&>(name));
    set_name(std::move(name));
    ```
    **but should do like below**
    ```
    void set_name(std::string name);
    set_name(std::move(name));
    ```
