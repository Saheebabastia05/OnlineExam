import java.util.*;

class User {
    private String username;
    private String password;
    
    public User(String username, String password) {
        this.username = username;
        this.password = password;
    }
    
    public String getUsername() {
        return username;
    }
    
    public String getPassword() {
        return password;
    }
}


class AuthenticationService {
    private Map<String, String> credentials; 
    
    public AuthenticationService() {
        credentials = new HashMap<>();
        
        credentials.put("Saheeba", "password1");
        credentials.put("Nitesh", "password2");
    }
    
    public boolean authenticate(String username, String password) {
        return credentials.containsKey(username) && credentials.get(username).equals(password);
    }
}

class Question {
    private String questionText;
    private String[] options;
    private int correctOptionIndex;
    
    public Question(String questionText, String[] options, int correctOptionIndex) {
        this.questionText = questionText;
        this.options = options;
        this.correctOptionIndex = correctOptionIndex;
    }
    
    public String getQuestionText() {
        return questionText;
    }
    
    public String[] getOptions() {
        return options;
    }
    
    public int getCorrectOptionIndex() {
        return correctOptionIndex;
    }
}


class Exam {
    private List<Question> questions;
    
    public Exam(List<Question> questions) {
        this.questions = questions;
    }
    
    public List<Question> getQuestions() {
        return questions;
    }
}

public class mainapplication {
    public static void main(String[] args) {
        AuthenticationService authService = new AuthenticationService();
        
        
        System.out.println("Welcome to the Online Examination System");
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter username: ");
        String username = scanner.nextLine();
        System.out.print("Enter password: ");
        String password = scanner.nextLine();
        
        if (authService.authenticate(username, password)) {
            System.out.println("Authentication successful!");
            
            
            List<Question> sampleQuestions = new ArrayList<>();
            sampleQuestions.add(new Question("What is the capital of India?", new String[]{"A. Odisha", "B. Delhi", "C. Goa", "D. Kerela"}, 1));
            sampleQuestions.add(new Question("Which planet is known as the Red Planet?", new String[]{"A. Venus", "B. Mars", "C. Jupiter", "D. Saturn"}, 1));
            sampleQuestions.add(new Question("Who wrote 'Merchant of Venice'?", new String[]{"A. William Shakespeare", "B. Charles Dickens", "C. Jane Austen", "D. Leo Tolstoy"}, 0));
            
            Exam exam = new Exam(sampleQuestions);
            
            System.out.println("\nWelcome to the Exam");
            List<Question> questions = exam.getQuestions();
            int score = 0;
            
            for (int i = 0; i < questions.size(); i++) {
                Question q = questions.get(i);
                System.out.println("\nQuestion " + (i + 1) + ": " + q.getQuestionText());
                String[] options = q.getOptions();
                for (String option : options) {
                    System.out.println(option);
                }
                System.out.print("Enter your answer (A/B/C/D): ");
                String userAnswer = scanner.nextLine();
                int userAnswerIndex = -1;
                switch (userAnswer.toUpperCase()) {
                    case "A":
                        userAnswerIndex = 0;
                        break;
                    case "B":
                        userAnswerIndex = 1;
                        break;
                    case "C":
                        userAnswerIndex = 2;
                        break;
                    case "D":
                        userAnswerIndex = 3;
                        break; 
                    default:
                        break;
                }
                
                if (userAnswerIndex == q.getCorrectOptionIndex()) {
                    System.out.println("Correct!");
                    score++;
                } else {
                    System.out.println("Incorrect!");
                }
            }
            
             
            System.out.println("\nExam complete!");
            System.out.println("Your score: " + score + " out of " + questions.size());
            
        } else {
            System.out.println("Authentication failed. Invalid username/password.");
        }
        
        scanner.close();
    }
}
