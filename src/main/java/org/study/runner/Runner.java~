package org.study.runner;

import org.study.entity.Group;
import org.study.entity.Student;

import javax.persistence.EntityManager;
import javax.persistence.EntityManagerFactory;
import javax.persistence.Persistence;
import javax.persistence.Query;
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;

/*
    1. Вывести на экран список групп с
    указанием количества студентов
    в каждой группе.
 */
public class Runner {

    public static void main(String[] args) {
        EntityManagerFactory emf = Persistence.createEntityManagerFactory("GroupPU");
        EntityManager em = emf.createEntityManager();

        List<Group> groups = generateRandomData();
        em.getTransaction().begin();
        try {
            for(int i = 0; i < groups.size(); i++) {
                em.persist(groups.get(i));
            }
            em.getTransaction().commit();
        } catch (Exception e) {
            em.getTransaction().rollback();
            return;
        }

        Query query = em.createQuery("Select g from groups g");
        List<Group> groupsFromDB = query.getResultList();
        System.out.println("List of groups:");
        for (int i = 0; i < groupsFromDB.size(); i++) {
            System.out.println(
                    String.format("#%d %s has %d student(s)", i, groupsFromDB.get(i).getName(), groupsFromDB.get(i).getStudents().size()));
        }

        em.close();
        emf.close();
    }

    private static List<Group> generateRandomData() {
        List<Group> groups = new LinkedList<>();

        for(int i = 0; i < 5; i++) {
            groups.add(new Group("group-"+i));
            List<Student> students = new ArrayList<>();
            for(int j = 0; j < Math.random()*25; j++) {
                students.add(new Student("student-"+i+j));
            }
            groups.get(i).setStudents(students);
        }
        return groups;
    }
}
