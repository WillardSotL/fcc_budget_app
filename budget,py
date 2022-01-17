class Category():
    def __init__(self, category):
        self.ledger = []
        self.draws = 0
        self.category = category
        self.balance = 0

    def get_balance(self):
        return self.balance

    def withdraws(self):
        return self.draws

    def deposit(self, amount, description=""):
        self.balance += amount
        self.ledger.append({"amount": amount, "description": description})
        return self

    def check_funds(self, amount):
        if self.balance >= amount:
            return True
        else:
            return False

    def withdraw(self, amount, description=""):
        if self.check_funds(amount):
            self.balance -= amount
            self.draws +=amount
            self.ledger.append({"amount": -amount, "description": description})
            return True
        else:
            return False

    def transfer(self, amount, category):
        if self.check_funds(amount):
            self.balance -= amount
            category.balance += amount
            self.ledger.append({"amount": -amount, "description": f"Transfer to {category.category}"})
            category.ledger.append({"amount": amount, "description": f"Transfer from {self.category}"})
            return True
        else:
            return False

    def __repr__(self):
        body = ""
        title = str(self.category).center(30, "*")
        balance = "{:.2f}".format(self.balance)
        total = '%.30s' % f"Total: {balance}"
        for lines in self.ledger:
            value = f'%.7s' % str("{:.2f}".format(list(lines.values())[0]))
            item = '%.23s' % list(lines.values())[1]
            line = item.ljust(23, " ") + value.rjust(7, " ")
            body += "\n" + line
        return f"{title}{body}\n{total}"

def create_spend_chart(categories):
    category_spend = []
    names_list = []
    if len(categories) > 4:
        return "Number of categories must not be more than 4"
    total_spent = 0
    longest_name = 0
    percentage = []

    # Returns list of names
    for cat in categories:
        names = cat.category
        names_list.append(names)

    # Returns list of spends
    for spend in categories:
        spend = spend.withdraws()
        category_spend.append(spend)
        total_spent += spend

    #calculating and storing the percentage of each pending category
    for num in category_spend:
        percent = 100.0 * (num / total_spent)
        percentage.append(percent)

    # Creating y-axis
    y = list((range(0, 110, 10)))
    y.sort(reverse=True)
    y_axis=[]
    graph = "Percentage spent by category\n"

    #storing numbers with a | and adding histogram
    for i_y in y:
        ys = f"{i_y}| ".rjust(5)
        yp = ""
        for n in percentage:
            if n >= i_y:
                yp += "o  "
            else:
                yp += "   "
        ysp = ys + yp
        y_axis.append(ysp)

    #printing rows of the graph
    for i_y_axis in y_axis:
        graph += f"{i_y_axis}\n"

    #printing x-axis of graph
    graph += 4 * " " + (3 * len(names_list) + 1) * '-' + "\n"

    #finding the length of the longest name
    for name in names_list:
        if len(name) > longest_name:
            longest_name = len(name)

    #returning the 1st to ith number to create the x-axis labels
    for i in range(longest_name):
        graph += "     "
        for name in names_list:
            if len(name) > i:
                graph += name[i] + "  "
            else:
                graph += "   "
        if i < longest_name -1:
            graph += "\n"

    return graph
