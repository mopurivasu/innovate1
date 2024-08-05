public class PersonalInformation {
    private String name;
    private String email;
    private String phone;

    public PersonalInformation(String name, String email, String phone) {
        this.name = name;
        this.email = email;
        this.phone = phone;
    }

    public String getName() {
        return name;
    }

    public String getEmail() {
        return email;
    }

    public String getPhone() {
        return phone;
    }

    @Override
    public String toString() {
        return "Name: " + name + "\nEmail: " + email + "\nPhone: " + phone;
    }
}
public class Education {
    private String degree;
    private String institution;
    private String yearOfGraduation;

    public Education(String degree, String institution, String yearOfGraduation) {
        this.degree = degree;
        this.institution = institution;
        this.yearOfGraduation = yearOfGraduation;
    }

    public String getDegree() {
        return degree;
    }

    public String getInstitution() {
        return institution;
    }

    public String getYearOfGraduation() {
        return yearOfGraduation;
    }

    @Override
    public String toString() {
        return degree + " from " + institution + " (Graduated: " + yearOfGraduation + ")";
    }
}
public class WorkExperience {
    private String jobTitle;
    private String company;
    private String duration;

    public WorkExperience(String jobTitle, String company, String duration) {
        this.jobTitle = jobTitle;
        this.company = company;
        this.duration = duration;
    }

    public String getJobTitle() {
        return jobTitle;
    }

    public String getCompany() {
        return company;
    }

    public String getDuration() {
        return duration;
    }

    @Override
    public String toString() {
        return jobTitle + " at " + company + " (" + duration + ")";
    }
}
import java.util.ArrayList;
import java.util.List;

public class Resume {
    private PersonalInformation personalInformation;
    private List<Education> educationList;
    private List<WorkExperience> workExperienceList;

    public Resume() {
        educationList = new ArrayList<>();
        workExperienceList = new ArrayList<>();
    }

    public void setPersonalInformation(PersonalInformation personalInformation) {
        this.personalInformation = personalInformation;
    }

    public void addEducation(Education education) {
        educationList.add(education);
    }

    public void addWorkExperience(WorkExperience workExperience) {
        workExperienceList.add(workExperience);
    }

    public void generateResume() {
        StringBuilder resume = new StringBuilder();
        resume.append("----- Resume -----\n");
        
        resume.append("\nPersonal Information:\n");
        resume.append(personalInformation.toString()).append("\n");
        
        resume.append("\nEducation:\n");
        for (Education education : educationList) {
            resume.append(education.toString()).append("\n");
        }
        
        resume.append("\nWork Experience:\n");
        for (WorkExperience workExperience : workExperienceList) {
            resume.append(workExperience.toString()).append("\n");
        }

        System.out.println(resume.toString());
    }
}
import java.util.Scanner;

public class ResumeBuilderApp {

    public static void main(String[] args) {
        Resume resume = new Resume();
        Scanner scanner = new Scanner(System.in);

        System.out.println("Welcome to the Resume Builder!");

        // Collect personal information
        System.out.print("Enter your name: ");
        String name = scanner.nextLine();
        System.out.print("Enter your email: ");
        String email = scanner.nextLine();
        System.out.print("Enter your phone: ");
        String phone = scanner.nextLine();
        PersonalInformation personalInfo = new PersonalInformation(name, email, phone);
        resume.setPersonalInformation(personalInfo);

        // Collect education details
        System.out.print("How many education entries do you want to add? ");
        int numEducation = scanner.nextInt();
        scanner.nextLine(); // consume the newline
        for (int i = 0; i < numEducation; i++) {
            System.out.print("Enter degree: ");
            String degree = scanner.nextLine();
            System.out.print("Enter institution: ");
            String institution = scanner.nextLine();
            System.out.print("Enter year of graduation: ");
            String yearOfGraduation = scanner.nextLine();
            Education education = new Education(degree, institution, yearOfGraduation);
            resume.addEducation(education);
        }

        // Collect work experience details
        System.out.print("How many work experience entries do you want to add? ");
        int numWork = scanner.nextInt();
        scanner.nextLine(); // consume the newline
        for (int i = 0; i < numWork; i++) {
            System.out.print("Enter job title: ");
            String jobTitle = scanner.nextLine();
            System.out.print("Enter company: ");
            String company = scanner.nextLine();
            System.out.print("Enter duration: ");
            String duration = scanner.nextLine();
            WorkExperience workExperience = new WorkExperience(jobTitle, company, duration);
            resume.addWorkExperience(workExperience);
        }

        // Generate the resume
        resume.generateResume();

        scanner.close();
    }
}
