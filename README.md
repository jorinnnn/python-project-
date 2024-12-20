# python-project- 

class ExpenseTracker:
    def _init_(self):
        # Initialize with an empty dataframe for expenses
        self.expenses = pd.DataFrame(columns=['Date', 'Description', 'Category', 'Amount'])
    
    def add_expense(self, date, description, category, amount):
        # Add a new expense
        new_expense = pd.DataFrame([[date, description, category, amount]], 
                                   columns=['Date', 'Description', 'Category', 'Amount'])
        self.expenses = pd.concat([self.expenses, new_expense], ignore_index=True)
    
    def show_expenses(self):
        # Show all expenses
        print(self.expenses)
    
    def filter_by_category(self, category):
        # Filter expenses by category
        return self.expenses[self.expenses['Category'] == category]
    
    def plot_expenses(self):
        # Create a pie chart for expenses by category
        category_totals = self.expenses.groupby('Category')['Amount'].sum()
        category_totals.plot.pie(autopct='%1.1f%%')
        plt.title('Expenses by Category')
        plt.show()

# Example usage
tracker = ExpenseTracker()
tracker.add_expense('2024-12-01', 'Lunch', 'Food', 15)
tracker.add_expense('2024-12-02', 'Taxi', 'Transport', 30)
tracker.add_expense('2024-12-03', 'Movie', 'Entertainment', 20)

tracker.show_expenses()
tracker.plot_expenses()
