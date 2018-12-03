# lab2
package com.company;

import java.util.Scanner;
import java.util.Stack;

public class Main {

    static int Prec(char ch) {
        switch (ch)
        {
            case '+':
            case '-':
                return 1;

            case '*':
            case '/':
                return 2;

            case '^':
                return 3;
        }
        return -1;
    }



    public static void main(String[] args) {
	

        System.out.println("please input any POSTFIX for getting result POSTFIX");

        Scanner s=new Scanner(System.in);

        String exp=s.nextLine();
        System.out.println(infixToPostfix(exp));
    }

    private static String infixToPostfix(String exp) {


        String result = new String("");

        
        Stack<Character> stack = new Stack<Character>();

        for (int i = 0; i<exp.length(); ++i)
        {
            char c = exp.charAt(i);


            if (Character.isLetterOrDigit(c))
                result += c;
            else if (c == '(')
                stack.push(c);

        


            else if (exp.charAt(0) == ')'){

                System.out.println("EXPRESSION is INVALID ");
                break;
            }

            else if (c == ')')
            {
                while (!stack.isEmpty() && stack.peek() != '(')
                    result += stack.pop();

                if (!stack.isEmpty() && stack.peek() != '(')
                    return "Invalid Expression";              
                else
                    stack.pop();
            }

            else 
            {
                while (!stack.isEmpty() && Prec(c) <= Prec(stack.peek()))
                    result += stack.pop();
                stack.push(c);
            }

        }

    
        while (!stack.isEmpty())
            result += stack.pop();

        return result;
    }


}


